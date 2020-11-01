# PyEnv Project Initialisation

For example the project need Python version 3.7.5.
To check the current **pyenv** Python version use

```bash
pyenv versions
```

## If the version does not exist

```bash
pyenv install -l     # to see all the available
pyenv install 3.7    # to see the available 3.7.x
pyenv install 3.7.5  # to install the version
```

## Set this version as local

```bash
cd project_folder
pyenv local 3.7.5  # has to be already installed!!!
```

This will create the file **.python-version** with content 3.7.5

## Check the current Python version

```bash
pyenv version
pyenv local
python --version
```

All the results has to be the same (3.7.5)
