# [Visual Studio Code with Python, pyenv and pylint](https://ondrejzeman.com/blog/vscode-python-pyenv-and-pylint)

This howto is written for the following scenario ...

    You run Debian or Ubuntu linux
    You have already installed Visual Studio Code
    Pyenv is installed in ***/home/USERNAME/.pyenv/*** (i.e. pyenv's recommended path)
    Your hypothetical project is in /home/USERNAME/my-project/
    ... and this project needs to run Python 3.8.1 so you have installed it by running ***pyenv install 3.8.1***.
    Pylint is installed as a system package (***apt-get install python3-pylint***).

Install the Visual Studio Code Python plugin

In VSCode, go to File > Preferences > Extensions. Look for an extension called Python with the identifier ms-python.python; install and enable it. If you prefer, the installation can also be done, faster, from command line - just run ...

code --install-extension ms-python.python

Point Visual Studio Code to the right Python interpreter

In VSCode's View menu, select Command Palette and search for Preferences: Open Workspace Settings (JSON). Selecting that option will create and open your project's .vscode/settings.json for editing.

{
    "python.pythonPath": "/home/USERNAME/.pyenv/versions/3.8.1/bin/python3",
}

Save the updated file. To confirm that your switch to Python 3.8.1 was successful, open VSCode's terminal (View > Terminal) and run ...

python -V

The output should say ...

Python 3.8.1

Configure Visual Studio Code to use pylint

At this point, VSCode will start complaining that pylint is not installed. That's because it assumes it to be among your project's packages. That's not the case here, so let's go back to your project's .vscode/settings.json and tell VSCode to use the pylint3 you've installed earlier:

{
    "python.pythonPath": "/home/USERNAME/.pyenv/versions/3.8.1/bin/python3",

    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.pylintPath": "/usr/bin/pylint3",
}

With this configuration, pylint will work - but it will now show you errors about imports. That's because it doesn't know which Python version you're using and where its packages are. Here's how you can tell it that:

{
    "python.pythonPath": "/home/USERNAME/.pyenv/versions/3.8.1/bin/python3",

    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.linting.pylintPath": "/usr/bin/pylint3",

    "python.linting.pylintArgs": [
        "--init-hook",
        "import sys; sys.path.append(\"/home/USERNAME/.pyenv/versions/3.8.1/lib/python3.8/site-packages\");",
    ]
}

Make sure the include the backslashes in the value for --init-hook - it won't work without them.

Save the file, and that's it! With this setup, VSCode will find your pylint executable and look for your packages in the right place.

Happy coding.
Posted June 12, 2020, updated Sept. 23, 2020
