# My Python Virtual Environment

## pyenv

I use ***pyenv-win*** for setting the Python version. In the project directory can check the local python (see file .python-version)

```bash
# to see the used   python version
pyenv version
# to see the local  python version
pyenv local
# to see the global python version
pyenv global
# to see the installed versions
python versions

# To view a list of python versions supported by pyenv windows
pyenv install -l
# to install version
pyenv install 3.7.7
# or for win64
pyenv install 3.7.7-amd64

# to uninstall version
pyenv uninstall 3.7.7-amd64

# ALWAYS REFRESH THE INSTALLATION
pyenv rehash
```

## venv

```bash
# On Ubuntu/Debian systems you need to install 
sudo apt-get install python3-venv
```

```bash
# Set aliases for veset & veactivate
sudo echo 'alias veset="python -m venv .venv"' >> ~/.bashrc
sudo echo 'alias veactivate="source .venv/bin/activate"' >> ~/.bashrc
source  ~/.bashrc
```

```bash
# In every project run first time
veset      #in  ~/.bash_aliases -> alias veset="python -m venv .venv"

# ACTIVATE it
# on Windows
.venv\Scripts\activate.bat

#on Linux
veactivate    #in  ~/.bash_aliases -> alias veactivate="source .venv/bin/activate"


# DEACTIVATE it
(.venv) $ deactivate
```

## pip

```bash
# Pip installation and update
(.venv) $ python -m pip install --upgrade pip

# Package installation
(.venv) $ pip install requests==2.6.0
# Show package insversiontallation
(.venv) $ pip show requests
# Package upgrade last version
(.venv) $ pip install --upgrade requests
# Package uninstall followed from list of packages
(.venv) $ pip uninstall requests

# List of installed packages
(.venv) $ pip list
# Freeze
(.venv) $ pip freeze > requirements.txt
# Cat (Windows Type) requirements.txt
(.venv) $ cat requirements.txt
(.venv) $ type requirements.txt
```

The requirements.txt can then be committed to version control and shipped as part of an application. Users can then install all the necessary packages with install -r:

```bash
(.venv) $ pip install -r requirements.txt
...
```

## gitignore

.venv

```bash
.venv

# pyenv
#   For a library or package, you might want to ignore these files since the code is
#   intended to run in multiple environments; otherwise, check them in:
# .python-version
```
