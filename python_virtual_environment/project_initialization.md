# Project Initialization

```bash
#Create a project folder if does not exist
mkdir project_folder

#Go to the project folder
cd project_folder
```

## git Initialization

Create a new GitHub repo with Python .gitignore
Then

```bash
git init
git remote add origin git@github.com:reedcouk/repository.git
git pull origin master
```

## pyenv Initialization

Use **_pyenv_** for setting the Python version.

For existing project with **.python-version** file you have to check with

```bash
pyenv version
pyenv local
python --version
```

If the two commands return the correct version we are ready with **_pyenv_**

- Initialazing the correct Python version

For example Python 3.7.7

```bash
# check the installed pyenv python versions
pyenv versions

# If the python version is missing then check the full list and install it
pyenv install -l
pyenv install 3.7.7

# Set this version for the project
pyenv local 3.7.7             # this will create the file .python-version

# ALWAYS REFRESH THE INSTALLATION
pyenv rehash

# Check the current Python version
pyenv version
pyenv local
python --version
# all of them have to show the same version
```

## venv Initialization

After the **_pyenv_** initialization

```bash
veset
```

## pip Initialization

```bash
# activate venv
$ veactivate
# upgrade pip
(.venv) $ python -m pip install --upgrade pip
```

```bash
# Now we can install the packages included in requirements.txt
(.venv) $ pip install -r requirements.txt
# or individual packages like
(.venv) $ pip install requests==2.6.0
```

## Closing the Initialization

- Git closing

```
git commit -a -m "Importing all the code"
git push origin master
```

- venv Deactivation

```bash
# deactivate venv
(.venv) $ deactivate

$...
```

Now we can go for a regular use of the project.
