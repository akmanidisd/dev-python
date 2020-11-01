# PyEnv System Installation

## Installing PyEnv

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
source ~/.bash_profile
```

The installation of pyenv is now complete.

## Installing System Libraries that are used by PyEnv during the "Python Installation"

```bash
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev
```

## Installing Python

Install with pyenv the versions that you are going to use and **_ignore the system version_**.<br/>
_Always use the pyenv installed versions only_.

For example:

1. installing Python 3.8.6, 3.7.9

```bash
pyenv install 3.8.6
pyenv install 3.7.9
pyenv versions
```

2. Setting 3.8.6 as global.

```bash
pyenv global 3.8.6
```

This will create the file **~/.python-version** with content 3.8.6
