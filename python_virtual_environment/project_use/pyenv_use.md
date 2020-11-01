# PyEnv Use

## PyEnv Most Used Commands

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

- To view a list of python versions supported by pyenv: **_pyenv install -l_**
- To install a python version: **_pyenv install 3.8.6_**
- To set a python version as the global version: **_pyenv global 3.8.6_**.<br/>
  This is the version of python that will be used by default if a local version (see below) isn't set.<br/>Note: _The version must first be installed_
- To set a python version as the local version: **_pyenv local 3.7.9_**. <br/>The version given will be used whenever python is called from within this folder. <br/>Note: _The version must first be installed_
- After (un)installing any python version, you must run **_pyenv rehash_** to update pyenv with the new python version.<br/>Note: This must be run outside of the .pyenv folder
- To uninstall a python version: **_pyenv uninstall 3.7.9_**
- To view which python you are using and its path: **_pyenv version_**
- To view all the python versions installed on this system: **_pyenv versions_**
