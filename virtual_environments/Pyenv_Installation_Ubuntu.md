# pyenv Ubuntu installation

<https://github.com/pyenv/pyenv>

## Basic GitHub Checkout

This will get you going with the latest version of pyenv and make it easy to fork and contribute any changes back upstream.

## Check out pyenv where you want it installed

A good place to choose is $HOME/.pyenv (but you can install it somewhere else).

```bah
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

## Define environment variable PYENV_ROOT

***PYENV_ROOT*** has to point to the path where pyenv repo is cloned and add ***$PYENV_ROOT/bin*** to your ***$PATH*** for access to the ***pyenv*** command-line utility.

### For bash

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
```

### For Ubuntu Desktop

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
```

## Add ***pyenv*** init to your shell

Please make sure eval "$(pyenv init -)" is placed toward the end of the shell configuration file since it manipulates PATH during the initialization.

```bash
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
```

or

```bash UBUNTU
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
```

**Ubuntu**: Modify your ***~/.bashrc*** file instead of ***~/.bash_profile***.

In Ubunto 20.04 there is no ***python*** but only ***python3***. Run the following command to create a symlink:

```bash
sudo ln -s /usr/bin/python3 /usr/bin/python
```

**General warning**: There are some systems where the BASH_ENV variable is configured to point to .bashrc. On such systems you should almost certainly put the above mentioned line eval "$(pyenv init -)" into .bash_profile, and not into .bashrc. Otherwise you may observe strange behaviour, such as pyenv getting into an infinite loop. See #264 for details.

## Restart your shell

The path changes take effect. You can now begin using pyenv.

```bash
exec "$SHELL"
```

## Install Python build dependencies

Before attempting to install a new Python version.

```bash
sudo apt-get update; sudo apt-get install --no-install-recommends make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

## Install Python versions

into $(pyenv root)/versions. For example, to download and install Python 3.7.7, run:

```bash
pyenv install 3.7.7
```

## Upgraing pyenv

cd $(pyenv root)
git pull

## Advanced Configuration

Rehashes shims. From time to time you'll need to rebuild your shim files. Doing this on init makes sure ***everything is up to date***. You can always run:

```bash
pyenv rehash
```

## Uninstalling pyenv

+ The simplicity of pyenv makes it easy to temporarily disable it, or uninstall from the system.

To **disable** ***pyenv*** managing your Python versions, simply remove the pyenv init line from your shell startup configuration. This will remove ***pyenv shims*** directory from PATH, and future invocations like python will execute the system Python version, as before pyenv.

***pyenv*** will still be accessible on the command line, but your Python apps won't be affected by version switching.

+ To completely uninstall pyenv, perform step (1) and then remove its root directory. This will delete all Python versions that were installed under ***$(pyenv root)/versions/*** directory:

```bash
rm -rf $(pyenv root)
```
