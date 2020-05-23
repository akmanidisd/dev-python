# Virtual Environments and Packages

## Creating Virtual Environments (venv)

```bash
python -m venv .venv
```

This will create the ***.venv*** directory if it doesn’t exist, and also create directories inside it containing a copy of the Python interpreter, the standard library, and various supporting files.

Once you’ve created a virtual environment, you may activate it.

```bash
# on Windows
.venv\Scripts\activate.bat

#on Linux
source .venv/bin/activate
```

Activating the virtual environment will change your shell’s prompt to show what virtual environment you’re using, and modify the environment so that running **python** will get you that particular version and installation of Python. For example:

```bash
(.venv) $ python
Python 3.5.1 (default, May  6 2016, 10:59:36)
  ...
>>> import sys
>>> sys.path

>>>
```

### Deactivating virtual environment

```bash
(.venv) $ deactivate

$...
```

The shell’s prompt stops showing the virtual environment

### Deactivating virtual environment

```bash
(.venv) $ deactivate

$...
```

The shell’s prompt stops showing the virtual environment

## Managing Packages with pip

Pip installation and update

```bash
(.venv) $ python -m pip install --upgrade pip
```

Pip has a number of subcommands: “search”, “install”, “uninstall”, “freeze”, etc. (Consult the Installing Python Modules guide for complete documentation for pip.) You can install, upgrade, and remove packages using pip. By default pip will install packages from the Python Package Index, <https://pypi.org>. You can browse the Python Package Index by going to it in your web browser, or you can use pip’s limited search feature:

Examples:

```bash
(.venv) $ pip search astronomy
skyfield               - Elegant astronomy for Python
gary                   - Galactic astronomy and gravitational dynamics.
novas                  - The United States Naval Observatory NOVAS astronomy library
astroobs               - Provides astronomy ephemeris to plan telescope observations
PyAstronomy            - A collection of astronomy related tools for Python.
...

(.venv) $ pip install requests==2.6.0
Collecting requests==2.6.0
  Using cached requests-2.6.0-py2.py3-none-any.whl
Installing collected packages: requests
Successfully installed requests-2.6.0

(.venv) $ pip install --upgrade requests
Collecting requests
...
Successfully installed certifi-2020.4.5.1 chardet-3.0.4 idna-2.9
requests-2.23.0 ...
```

***pip uninstall*** followed by one or more package names will remove the packages from the virtual environment.

pip show will display information about a particular package:

```bash
(.venv) $ pip show requests
Name: requests
Version: 2.23.0
Summary: Python HTTP for Humans.
....
Requires: idna, urllib3, certifi, chardet
....
```

pip list will display all of the packages installed in the virtual environment:

```bash
(.venv) $ pip list
Package    Version
---------- ----------
certifi    2020.4.5.1
chardet    3.0.4
idna       2.9
pip        20.1.1
requests   2.23.0
setuptools 41.2.0
urllib3    1.25.9
```

pip freeze will produce a similar list of the installed packages, but the output uses the format that pip install expects. A common convention is to put this list in a requirements.txt file:

```bash
(.venv) $ pip freeze > requirements.txt

(.venv) $ type requirements.txt
certifi==2020.4.5.1
chardet==3.0.4
idna==2.9
requests==2.23.0
urllib3==1.25.9
```

The requirements.txt can then be committed to version control and shipped as part of an application. Users can then install all the necessary packages with install -r:

```bash
(.venv) $ pip install -r requirements.txt
...
```

## Deactivating virtual environment

```bash
(.venv) $ deactivate

$...
```

The shell’s prompt stops showing the virtual environment
