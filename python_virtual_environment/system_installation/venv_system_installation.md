# venv System Installation

On Ubuntu/Debian **_venv_** is not preinstalled.

```bash
sudo apt-get install python3-venv
```

Then create aliases for:

- _veset_ (set virtual environment)
- _veactivate_ (activate virtual environment)

```bash
# Add aliases for veset & veactivate in ~/.bash_aliases
alias veset="python -m venv .venv"
alias veactivate="source .venv/bin/activate"

# add these lines if not exist in  ~/.bash_profile
if [ -f ~/.bash_aliases ]; then
. ~/.bash_aliases
fi

# activate
source  ~/.bash_profile
```
