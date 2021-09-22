# MacBook Pro Set Up 

This document contains instructions for setting up a MacBook Pro in B.C. Government, tailored for data science workflows used by the Data Science Partnerships team.  The document is organized with least complex steps at the top (i.e. point and click downloads) leading to tools that require more advanced setup at the bottom. Some of the setup instructions assume a working knowledge of Unix/Linux. 

*README*: Take care to vet whether the setup advice is relevant (or still relevant) for your OS or machine, and to ensure knowledge of and keeping with the bcgov [Appropriate Use Policy](https://www2.gov.bc.ca/gov/content?id=33A6DE0643E54676B21033E5DA8E03CF).


## Point & Click Software

- [R](https://www.r-project.org/)  - more setup information further down
- [RStudio](https://www.rstudio.com/) - requires R 3.0.1 or higher (as of Sept. 2021)
- [Visual Studio Code](https://code.visualstudio.com/)
  - [Extensions](https://code.visualstudio.com/docs/editor/extension-marketplace) (Docker, Python, R, Git History)
  - [Enable launching](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line) from the terminal via the `code` command
- [Trello](https://trello.com/)\*
- [Microsoft Remote Desktop](https://apps.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12)\*
- [Skype for Business](https://support.office.com/en-us/article/Install-Skype-for-Business-8a0d4da8-9d58-44f9-9759-5c8f340cb3fb?ui=en-US&rs=en-US&ad=US#OS_Type=Mac)\*\*
- Cisco AnyConnect VPN - Remote Access User Guide and download link for AnyConnect on the [Remote Access Services Page](https://ssbc-client.gov.bc.ca/services/remoteaccess/documents.htm)\*\*

\*    Available from the Mac App Store
</br>
\*\*  Should be pre-installed on setup

The following are optional to be download as/if needed:

- [Inkscape](https://inkscape.org/en/)
- [Docker](https://www.docker.com/)
- [Git Kraken](https://www.gitkraken.com/) - visual git tool


## Software Set Up & Tweaks

#### MacBook 
- [Customize the touchbar](https://support.apple.com/en-ca/guide/mac-help/mchl5a63b060/mac), for example adding the Lock Screen button for quick access/use

#### Changing IDIR Password:
TO DO

#### Safari:
- Safari > Preferences > Advanced > Show full website address
- Safari > Preferences > Advanced > Show Develop menu
- Safari > View > Show status bar

#### Finder:
- Show [dotfiles](http://www.macosxtips.co.uk/index_files/quickly-show-hidden-files.php)
  - one time: Cmd + Shift + `.` 
  - to show them all the time: (from Terminal)
      `defaults write com.apple.finder AppleShowAllFiles -bool YES; killall Finder`
  - to hide them again: (from Terminal)
     `defaults write com.apple.finder AppleShowAllFiles -bool NO; killall Finder`
- Prevent `._DStore` files from being created on network shares:
   - `defaults write com.apple.desktopservices DSDontWriteNetworkStores true`
- [Customize the Finder toolbar and sidebar](https://support.apple.com/en-ca/guide/mac-help/mchlp3011/mac)

#### Alfred:

The [Alfred App](https://www.alfredapp.com/) is super handy for quickly opening files/folders. You can see a demo and how to tailor the App in this YouTube video [here](https://www.youtube.com/watch?v=boKFxBniUH0). To enable it open Rstudio projects you can "register" the .Rproj file type with Alfred. 

 - Go to Alfred’s Preferences > Features > Default Results > Advanced…. 
 - Drag any .Rproj file onto this space and then close.

#### Terminal:
Enable New Terminal at Folder: System Preferences > Keyboard > Shortcuts > Services (from [here](https://stackoverflow.com/questions/420456/open-terminal-here-in-mac-os-finder))

You can make your terminal prettier (and more productive) in many ways...one popular terminal alternative is [iTerm2](https://www.iterm2.com/). Here is [one example](https://www.freecodecamp.org/news/jazz-up-your-zsh-terminal-in-seven-steps-a-visual-guide-e81a8fd59a38/) of how to use iTerm2 with the zsh shell (now the default in macOS Catalina and Big Sur) and Oh-My-ZSH.


## R & RStudio

**Note:** It's handy to save your personal dotfiles and transfer them 
to you new computer (after reviewing them to make sure they are doing what you want them to). Some of these may contain sensitive information such as API keys so handle them with care. Some key dotfiles might be:

```
~/.Rprofile
~/.Renviron
~/.bashrc and/or ~./bash_profile
~/.zshrc
~/.config/ (various files and/or folders such as rstudio)
```

#### Set Up Local R Library Location

**If not already set in your personal `.Renviron` file**

```
cd && mkdir Rlibrary
echo R_LIBS=~/Rlibrary >> .Renviron
```

#### Recommended RStudio Global Defaults
RStudio >> Tools >> Global Options >> General >> Basic:

- untick `Restore .RData into workspace at startup`
- `Save workspace to .RData on exit: <NEVER>`

RStudio >> Tools >> Global Options >> General >> Advanced:

- tick `Show .Last.value in environment listing`


#### Install R Build Tools:
Install the appropriate `gfortran` for compiling packages from source. As of Sept 2021, the correct gfortran to install is [version 8.2](https://github.com/fxcoudert/gfortran-for-macOS/releases/tag/8.2) (for all macOS versions including Big Sur, even though it's labelled 'Mojave').
- More detailed installation instructions and link to download: https://thecoatlessprofessor.com/programming/cpp/r-compiler-tools-for-rcpp-on-macos/


## Homebrew

#### Installation:

Follow the most up-to-date installation instructions [here](https://brew.sh).

Installing Homebrew should also install the macOS Command Line Developer tools. You can verify this by typing:

```
xcode-select -p
```

If it doesn't give you an output like `/Library/Developer/CommandLineTools` you can install it with:

```
xcode-select --install
```

#### Homebrew Maintenance:
To update homebrew and check what packages are available to update:
```
brew update
```

To upgrade packages:
```
brew upgrade
```

To cleanup
```
brew cleanup
```

To help diagnose problems:
```
brew doctor
```

To do it all at once (this could take a while if big packages are updated)
```
brew update && brew upgrade && brew cleanup
```

## Git and GitHub

#### Git: Install and Configure [Git](https://git-scm.com/)

```
# install with homebrew:
brew install git
git config --global user.email firstname.lastname@gov.bc.ca
git config --global user.name "Firstname Lastname"
git config --global core.editor "nano"
git config --global credential.helper osxkeychain
```

#### GitHub: Set Up [GitHub](https://github.com/) Authorization

The simplest way to do this is actually through R. This process ensures that you are authenticated with GitHub for command-line use, as well as through RStudio and/or other git GUIs:

- Go to GitHub and [create a new Personal Access Token](https://github.com/settings/tokens) with repo, user, and gist access. Copy the key to your clipboard.
- In R:

```r
install.packages("gitcreds")
library(gitcreds)
gitcreds_set()
```

At the prompt, paste the key that you previously copied from GitHub.

In general, the online book [Happy Git with R](https://happygitwithr.com) provides the best and most up-to-date advice for working with R and Git/GitHub. To learn more about credential caching for git and more detailed instructions, see [this chapter](https://happygitwithr.com/credential-caching.html#credential-caching).



#### Install LaTeX

We are currently recommending (though still testing) installation of the [`TinyTex`](https://yihui.org/tinytex/)
`LaTeX` distribution, which is built especially for using with R:

```r
install.packages("tinytex")
install_tinytex()
```

This works great for R Markdown-oriented workflows, but also provides command-line
use for use outside R (though installation of packages must be done with `tlmgr` as no GUI exists as with MacTeX).

If you'd prefer to install the core Mac LaTeX distribution with a GUI, it's easiest to install `mactex` with Homebrew:

```
$ brew install --cask mactex
```

#### System Libraries for Common R Packages

These are mostly mostly taken from [Bob Rudis' blog](https://rud.is/b/2015/10/22/installing-r-on-os-x-100-homebrew-edition/).

Xquartz is a graphics device for R, for use for displaying graphics outside of RStudio (i.e., if you are using R from the command line or need to use the X11 graphics device. X11 is much faster than the RStudio graphics device so can be useful for large complex plots such as maps).

```
brew install xquartz
```

You may need to install some system libraries if you want to build packages from source (i.e., new releases or development versions from GitHub), or are developing packages that rely on system libraries. This is almost always best done via Homebrew.

Some common ones are: 

```
brew install libsvg curl libxml2 boost

## imagemagick for command-line image manipulation and use of the 'magick' R package
brew install imagemagick
```

#### Fonts

You might want to install some nice fonts that are suitable for code (e.g., with [ligatures](https://betterwebtype.com/articles/2020/02/13/5-monospaced-fonts-with-cool-coding-ligatures/)), which can also be done via Homebrew. For example, [Fira-code](https://github.com/tonsky/FiraCode) is a lovely coding font:

```
brew tap homebrew/cask-fonts
brew install font-fira-code
```

For more advanced setup tips and/or Geospatial software setup, see [Macbook Pro Setup - Advanced Setup and Geospatial Tools](Macbook-advanced-geo.md).
