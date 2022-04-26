[![img](https://img.shields.io/badge/Lifecycle-Maturing-007EC6)](https://github.com/bcgov/repomountie/blob/master/doc/lifecycle-badges.md)

## Steps to set-up a new Secure Environment remote machine and/or new project

1. Open Chrome 
   - [ ] Make Chrome default browser 
   - [ ] Import bookmarks from `R:/working/bookmarks_[latest-date].html
   - [ ] Pin Chrome to Taskbar
2. Go to GitLab in Chrome (via the new bookmarks) - sign in with `Pop Data Sso`
   - [ ] If this is a new project: Create a Personal Access Token (User Settings > Access Tokens) and save it in a text file in your private user directory (`U:/`) or `R:/[your-project-specific-username]` - these are the same directory, just mapped twice.
4. Open RStudio
   - [ ] Pin RStudio to Taskbar
   - [ ] Go to the repository for `dipr` in GitLab, and follow the instructions in the README to install `dipr`. This will prompt an authentication window where you type in your username and your PAT from step 2 as your password (if this is a new machine for an existing project, you should have your PAT in the text file you previously saved in step 2). Your gitlab credentials will now be stored for all git projects on this machine. 
   - [ ] *Note: if you entered your PAT incorrectly the incorrect credentials will be stored and you will be unable to interact with gitlab. You can a) change/reset it by opening Credential Manager in the Windows Control Panel and under "Windows Credentials" there will be a gitlab entry you can then edit or b) run `credentials::git_credential_update("https://projectsc.popdata.bc.ca")` in your R console.*
   - [ ] If you previously saved your Rstudio preferences in GitLab, restore them with `dipr::restore_rstudio_prefs)_`.
   - [ ] Otherwise change settings: Tools > Global Options
     1. General  
        - Change "Default working directory" to the directory you made in step 3.  
        - Uncheck "Restore .RData into workspace at startup  
        - Change "Save workspace to .RData on exit" to "Never"  
     2. Code, Appearance, and Pane Layout - adjust to your preferred configuration
5. Open Explorer - right-click and select Quick Access to pin 📌 folders you use frequently
