# Managing multiple Python versions and virtual environments

[link](https://www.freecodecamp.org/news/manage-multiple-python-versions-and-virtual-environments-venv-pyenv-pyvenv-a29fb00c296f/)

Here we’ll look at three different tools for working with these, and when you might need each one. Let’s explore the use cases for:

+ venv
+ pyenv

If you are using a single version of Python say version 3.3+, and want to manage different virtual environments, then ***venv*** is all you need.

If you want to use multiple versions of Python at 3.3+, with or without virtual environments, then continue to read about ***pyenv***.

## venv

From Python 3.3+ the ***venv*** package is included. It is ideal for creating lightweight virtual environments.

***venv*** is used to create a new environment via the terminal command:

```bash
$ python3 -m venv .venv
```

***.venv*** is the name of directory name to create.  To activate run:

```bash
# on Windows
.venv\Scripts\activate.bat

#on Linux
source .venv/bin/activate
```

and deactivated with simply:

```bash
deactivate
```

If you need to remove the environment completely after deactivating it, you can run:

```bash
rm -r name-given
```

By default, the environment it creates will be the current version of Python you are using. If you are writing documentation, and want the additional safety that the correct version of Python is being used by your reader you can specify the major and minor version number in the command, like so:

```bash
python3.6 -m venv .venv
```

If the reader is using a version other than 3.6 then the command will not be successful and will indicate in its error message. However, any patch version (for example 3.6.4) will work.

When the environment is active, any packages can be installed to it via ***pip*** as normal. By default, the newly created environment will not include any packages already installed on the machine. As ***pip*** itself will not necessarily be installed on the machine. It is recommended to first upgrade pip to the latest version, using:

```bash
pip install --upgrade pip
```

Projects will commonly have a ***requirements.txt*** file specifying its dependencies. This allows the shortcut command 

```bash
pip install -r requirements.txt 
```

command to quickly install all packages to the newly created virtual environment. They will only exist in the virtual environment. It will not be available when it is deactivated but will persist when it is reactivated.

If you do not need to use additional versions of Python itself, then this is all you need to create isolated, project specific, virtual environments.

## pyenv

If you wish to use multiple versions of Python on a single machine, then ***pyenv*** is a commonly used tool to install and switch between versions. It does not come bundled with Python and must be installed separately.

The pyenv [documentation](https://github.com/pyenv/pyenv) includes a great description of how it works, so here we will look simply at how to use it.

Firstly we will need to install it. 
The Windows version is subset of the Linux version.

Running 

```bash
pyenv versions 
```

will show which Python versions are currently installed, with a * next to the one currently in use. 

```bash
pyenv version
```

shows this directly, and

```bash
python --version
```

can be used to verify this.

To install an additional version, say 3.8.2, simply use

```bash
pyenv install 3.8.2

or for Windows x64

```bash
pyenv install 3.8.2-amd64
```

***pyenv*** looks in four places to decide which version of Python to use, in priority order:

+ The PYENV_VERSION environment variable (if specified). You can use the pyenv shell command to set this environment variable in your current shell session.
+ The application-specific .python-version file in the current directory (if present). You can modify the current directory's .python-version file with the pyenv local command.
+ The first .python-version file found (if any) by searching each parent directory, until reaching the root of your filesystem.
+ The global version file. You can modify this file using the pyenv global command. If the global version file is not present, pyenv assumes you want to use the "system" Python. (In other words, whatever version would run if pyenv weren't in your PATH.)

When setting up a new project that is to use Python 3.8.2 then 

```bash
pyenv local 3.6.4 
```

would be ran in its root directory. This would both set the version, and create a ***.python-version*** file, so that other contributors’ machines would pick it up.

The full [description of pyenv commands](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md) is one to bookmark.

## pyenv and venv

When working with Python 3.3+ we now know both how to install and switch between different versions of Python, and how to create new virtual environments.

As an example, let’s say we were setting up a project that was to use Python 3.7.

First we could set our local version using

```bash
pyenv local 3.7.0
```

If we then ran

```bash
python -m venv .venv
```

a new virtual environment would be set up under ***.venv***, using our locally enabled Python 3.7.0.

To activate run:

```bash
# on Windows
.venv\Scripts\activate.bat

#on Linux
source .venv/bin/activate
```

and can start working.

Next we could optionally document that a collaborator should use 

```bash
python3.7 -m venv .venv
```

This means even if a collaborator was not using ***pyenv*** the ***python3.7*** command would error if their Python version was not the same major and minor version (3 and 7), as we intended.

Alternatively, we could choose to simply specify that 3.7.0 was to be used, and instruct 

```bash
python3 -m venv .venv
```

If we believe that any version greater than 3.7 is acceptable, then we also may choose to use python3 over python3.7, as if the collaborator was using 3.8 then they would otherwise also receive an error. This is a project specific decision.
