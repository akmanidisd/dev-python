# INSTALLING PYENV

## Execution the following commands.

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
source ~/.bash_profile
```

Installation of pyenv is now complete.

## INSTALLING LIBRARIES THAT ARE NEEDED FOR "INSTALLING PYTHON"

Execution the following command.

```bash
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev
```

## INSTALLING PYTHON

Execution the following command, then setting Python version that will use.
In this case, installing Python 3.7.9.

```bash
pyenv install 3.7.9
pyenv install 3.8.6

pyenv global 3.8.6
# for projects
pyenv local 3.7.9

# To see the versions
pyenv versions   # all version
pyenv version    # current version
pyenv global
pyenv local
```
