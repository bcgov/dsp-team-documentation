# Macbook Pro Setup - Advanced Setup and Geospatial Tools

## Some shell/git tweaks

Add ~/bin to your path as a place to hold custom shell scripts, set editor to nano instead of vi. This is only relevant if you are using `bash` instead of `zsh`:

```
cat << EOF >> $HOME/.bashrc

# Set editor to nano instead of vi
export EDITOR="nano"

# put custom shell scripts etc in ~/bin dir, make sure available on PATH:
export PATH=$HOME/bin:$PATH"
EOF

cat << EOF >> $HOME/.bash_profile
if [ -f ~/.bashrc ]; then
   source ~/.bashrc
fi
EOF
```

#### Java
 *Hopefully you never need this, this has not been tested lately*
 
- Download and install the [Java 8 SDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
- In the terminal, type: `sudo R CMD javareconf`
- In R, type: `install.packages("rJava", type = "source")


## Python (Homebrew)

Our current recommendation is to use the [conda](https://conda.io) distribution of Python, installed with Homebrew. 

You can install the full [`anaconda`](https://docs.conda.io/projects/conda/en/latest/user-guide/install/download.html#anaconda-or-miniconda), which is very large and installs a lot of default python packages, or [`miniconda`](https://docs.conda.io/en/latest/miniconda.html) which is much lighter, requiring you to install more packages as you go.

```
brew install --cask miniconda # (or anaconda)
```

After installation is complete, run (as per instructions in the homebrew install) the following
to activate conda as your default Python:

```
conda init $(basename $SHELL)
conda config --set changeps1 false # so conda doesn't change your shell prompt
```

It is recommended to use [conda environments](https://conda.io/projects/conda/en/latest/user-guide/concepts/environments.html) when doing Python-based projects.


## QGIS 
#### Install [QGIS](http://qgis.org/en/site/)

```
brew install --cask qgis
```

## R Geospatial Tools

```
## mapshaper for editing Shapefile, GeoJSON, TopoJSON, CSV and several other data formats, written in JavaScript 
## We use the `rmapshaper` R package for most task but `rmapshaper` has a size limit

brew install node
npm install -g mapshaper

# R spatial stuff (sf etc. takes a long time) - only needed if you want or need to build sf from source
brew install pkg-config
brew install udunits
brew install gdal

# Install ESRI File GDB drivers so can write to .gdb
# requires you to add `export GDAL_DRIVER_PATH=/usr/local/lib/gdalplugins` to your PATH
brew tap osgeo/osgeo4mac && brew tap --repair
brew install osgeo-gdal-filegdb
```


## Extra stuff, probably not needed (until it is)

### OpenShift

#### Install [OpenShift](https://www.openshift.com/) command-line tools:

```
brew install openshift-cli
```

### PostgreSQL/PostGIS

#### Installation

```
brew install postgresql
brew install postgis
```

#### Set environment variables/aliases
Copy and paste (and hit return) the following script, which will set environment variables/create aliases that are used often for postgis stuff:

```
cat <<EOF >> $HOME/.bashrc
# save pg typing
export PGDATA=/usr/local/var/postgres
export PGHOST=localhost
export PGPORT=5432
# export PGDATABASE=postgis
export PGUSER=postgres

# Fiona wants PROJ_LIB set
export PROJ_LIB="/usr/local/share/proj"

alias pg_start='pg_ctl -D $PGDATA -l $PGDATA/server.log start'
alias pg_stop='pg_ctl -D $PGDATA stop -s -m fast'

# Add path to custom gdal drivers (ESRI File GDB)
export GDAL_DRIVER_PATH=/usr/local/lib/gdalplugins
EOF
```

#### Tune your postgresql installation:

These settings work well on a 2016 Macbook Pro with 16GB of memory. For more information on tuning, see the [postgresql tuning wiki](https://wiki.postgresql.org/wiki/Tuning_Your_PostgreSQL_Server).

Copy and paste this script in the terminal:

```
cat << EOF > /usr/local/var/postgres/pgtune.conf
log_timezone = 'Canada/Pacific'
datestyle = 'iso, mdy'
timezone = 'Canada/Pacific'
lc_messages = 'en_US.UTF-8'      # locale for system error message
lc_monetary = 'en_US.UTF-8'      # locale for monetary formatting
lc_numeric = 'en_US.UTF-8'      # locale for number formatting
lc_time = 'en_US.UTF-8'        # locale for time formatting
default_text_search_config = 'pg_catalog.english'
default_statistics_target = 100
log_min_duration_statement = 2000

max_connections = 100
max_locks_per_transaction = 64
dynamic_shared_memory_type = posix
checkpoint_timeout = 30min    # range 30s-1d
maintenance_work_mem = 2GB
effective_cache_size = 8GB
work_mem = 500MB
max_wal_size = 10GB
wal_buffers = 16MB
shared_buffers = 4GB # Min 128KB
EOF

cat << EOF >> /usr/local/var/postgres/postgresql.conf
# Include custom settings:
include = 'pgtune.conf'
EOF
```

And then this, to give more system memory (You will be prompted for your password):

```
sudo bash -c 'cat > /etc/sysctl.conf' << EOF
kern.sysv.shmmax=17179869184
kern.sysv.shmmin=1
kern.sysv.shmmni=32
kern.sysv.shmseg=8
kern.sysv.shmall=4194304
kern.maxprocperuid=512
kern.maxproc=2048
EOF
``` 

Then back in the terminal:
```
initdb -E utf8 -U postgres -W
# at the prompt, set superuser password to 'postgres'
pg_start # start the database (can stop any time with pg_stop)
```

## Sources:
- <https://rud.is/b/2015/10/22/installing-r-on-os-x-100-homebrew-edition/>
- <https://github.com/jennybc/system-setup>
- <https://github.com/r-spatial/sf#macos>
- <https://www.karambelkar.info/2017/01/setup-osx-for-r/>
- <https://github.com/adamhsparks/setup_macOS_for_R>
- Python: <https://www.davidculley.com/installing-python-on-a-mac/>
- Git user.email prompting: <http://depressiverobot.com/2015/01/05/git-email.html>
- Postgres/postgis:
    - <https://github.com/nvkelso/geo-how-to/wiki/Installing-Open-Source-Geo-Software:-Mac-Edition>
    - <https://www.postgresql.org/docs/10/static/kernel-resources.html>
    - <http://big-elephants.com/2012-12/tuning-postgres-on-macos/>
    - [Simon Norris](https://github.com/smnorris) of [Hillcrest Geographics](https://hillcrestgeo.ca/)
