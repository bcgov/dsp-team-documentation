## Steps in setting up a new SRE machine and/or new project

1. Open Chrome 
   1. Make Chrome default browser 
   2. Import bookmarks from `R:/working/bookmarks_[latest-date].html
   3. Pin Chrome to Taskbar
2. Go to GitLab in Chrome (via the new bookmarks) - sign in with `Pop Data Sso`
   1. If this is a new project: Create a Personal Access Token (User Settings > Access Tokens) and save it in a text file in your private user directory (`U:/`) or `R:/[your-project-specific-username]` - these are the same directory, just mapped twice.
3. Open Git Bash
   1. Pin Git Bash to Taskbar
   2. cd to `/R/working`. Create a user directory for your self with your first name in either `/R/working/` or `/R/working/users` depending on the convention of the project and `cd` into that directory. (e.g., `mkdir andy && cd andy`)
   3. If this is a new project, type `git clone https://projectsc.popdata.bc.ca/shares/dipr.git && cd dipr`. If an existing project (but a new machine), type `cd dipr && git pull`. This will prompt an authentication window where you type in your username and your PAT from step 2 as your password (if this is a new machine for an existing project, you should have your PAT in the text file you previously saved in step 2). Your gitlab credentials will now be stored for all git projects on this machine.
4. Open RStudio
   1. Pin RStudio to Taskbar
   2. Change settings:
      1. Tools > Global Options
         1. General
            1. Change "Default working directory" to the directory you made in step 3.
            2. Uncheck "Restore .RData into workspace at startup
            3. Change "Save workspace to .RData on exit" to "Never"
         2. Code, Appearance, and Pane Layout - adjust to your preferred configuration
      2. 
   3. Open the `dipr` project in RStudio (cloned in step 3) and type `devtools::install()` to install the package.