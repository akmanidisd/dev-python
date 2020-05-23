## pyenv-win commands

 ```text
   commands    List all available pyenv commands
   local       Set or show the local application-specific Python version
   global      Set or show the global Python version
   shell       Set or show the shell-specific Python version
   install     Install a Python version using python-build
   uninstall   Uninstall a specific Python version
   rehash      Rehash pyenv shims (run this after installing executables)
   version     Show the current Python version and its origin
   versions    List all Python versions available to pyenv
   exec        Runs an executable by first preparing PATH so that the selected Python
```

Usage

+ To view a list of python versions supported by pyenv windows: ***pyenv install -l***
+ To install a python version: ***pyenv install 3.5.2***
+ To set a python version as the global version: ***pyenv global 3.5.2***.<br/> 
This is the version of python that will be used by default if a local version (see below) isn't set.<br/>Note: *The version must first be installed*
+ To set a python version as the local version: ***pyenv local 3.5.2***. <br/>The version given will be used whenever python is called from within this folder. <br/>This is different than a virtual env, which needs to be explicitly activated.<br/>Note: *The version must first be installed*
+ After (un)installing any python version, you must run ***pyenv rehash*** to update pyenv with the new python version.  <br/>Note: This must be run outside of the .pyenv folder
+ To uninstall a python version: ***pyenv uninstall 3.5.2***
+ To view which python you are using and its path: ***pyenv version***
+ To view all the python versions installed on this system: ***pyenv versions***
