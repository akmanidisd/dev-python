# Pip

When the environment is active, any packages can be installed to it via ***pip*** as normal. By default, the newly created environment will not include any packages already installed on the machine. As ***pip*** itself will not necessarily be installed on the machine. It is recommended to first upgrade pip to the latest version, using:

```bash
python -m pip install --upgrade pip
```

Projects will commonly have a ***requirements.txt*** file specifying its dependencies. This allows the shortcut command

```bash
pip install -r requirements.txt
```

command to quickly install all packages to the newly created virtual environment. They will only exist in the virtual environment. It will not be available when it is deactivated but will persist when it is reactivated.

## Installing individual packages

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
# Cat requirements.txt
(.venv) $ cat requirements.txt
```

The requirements.txt can then be committed to version control and shipped as part of an application. Users can then install all the necessary packages with install -r:

```bash
(.venv) $ pip install -r requirements.txt
...
```

Uninstalling all listed packages

```bash
(.venv) $ pip freeze     > for_deletion.txt

(.venv) $ pip uninstall -r for_deletion.txt
# or
(.venv) $ pip uninstall -r for_deletion.txt -y

...
```
