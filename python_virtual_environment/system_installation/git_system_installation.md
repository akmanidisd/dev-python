# Git System Installation

Git comes with a tool called **_git config_** that lets you get and set configuration variables that control all aspects of how Git looks and operates. These variables can be stored in three different places:

1. **_/etc/gitconfig_** -> using **_--system_**<br/>
   Contains values applied to every user on the system and all their repositories. If you pass the option **_--system_** to git config, it reads and writes from this file specifically. (Because this is a system configuration file, you would need administrative or superuser privilege to make changes to it.)

2. **_~/.gitconfig_** or **_~/.config/git/config_** -> using **_--global_**<br/>
   Values specific personally to you, the user. You can make Git read and write to this file specifically by passing the **_--global_** option, and this affects all of the repositories you work with on your system.

3. **_.git/config_** -> using **_--local_**<br/>
   Config file in the Git directory of whatever repository you’re currently using: Specific to that single repository. You can force Git to read from and write to this file with the **_--local_** option, but that is in fact the default. (Unsurprisingly, you need to be located somewhere in a Git repository for this option to work properly.)

Each level overrides values in the previous level. Biggest priority have **_--local_** then **_--global_** and then **_--system_**.
We will use **_--global_** for user level and **_--local_** for repository/project level.

You can view all of your settings and where they are coming from using:
'''
git config --list --show-origin
'''

## On USER Level

On USER level use **_--global_**. The settings are stored in **_~/.gitconfig_** or **_~/.config/git/config_** file. This affects all of the repositories you work with on your system.

```
# Setting User Identity:
git config --global user.name "company-user-id"
git config --global user.email "company-user-email"

# Setting User Editor:
git config --global core.editor "code --wait"

# List User Config
git config --global --list

# View the config file using cat with the following command:
cat ~/.gitconfig
```

## GitHub

We have access to all the public and the company private repos in GitHub.
**https://github.com/reedcouk**
