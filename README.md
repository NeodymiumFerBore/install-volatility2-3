# install-volatility2-3

A simple playbook to install volatility 2 and 3 in their own venv, and make them accessible outside their venv with a symlink somewhere in your PATH (by default, `$HOME/.local/bin`).

## Usage

```sh
# Setup ansible in a venv if you dont have it already
$ python3 -m venv venv-ansible
$ source venv-ansible/bin/activate
$ python3 -m pip install ansible

# Clone this repository
$ git clone https://github.com/NeodymiumFerBore/install-volatility2-3.git
$ cd install-volatility2-3

# Run the playbook
$ ansible-playbook -i localhost, --ask-become-pass install_volatility.yaml

# Enjoy using volatility2, volatility3 and volshell
$ vol2
Volatility Foundation Volatility Framework 2.6.1
(...)

$ vol3
Volatility 3 Framework 2.4.2
usage: volatility [-h] [-c CONFIG] [--parallelism [{processes,threads,off}]] [-e EXTEND] [-p PLUGIN_DIRS] [-s SYMBOL_DIRS] [-v] [-l LOG] [-o OUTPUT_DIR] [-q]
                  [-r RENDERER] [-f FILE] [--write-config] [--save-config SAVE_CONFIG] [--clear-cache] [--cache-path CACHE_PATH] [--offline]
                  [--single-location SINGLE_LOCATION] [--stackers [STACKERS ...]] [--single-swap-locations [SINGLE_SWAP_LOCATIONS ...]]
                  plugin ...
volatility: error: Please select a plugin to run

$ volshell
Volshell (Volatility 3 Framework) 2.4.2
(...)
```

## Configuration

You can set 2 extra vars to customize the installation.

- `venv_path`: the path where both venv `volatility2` and `volatility3` will be created.
  - Default: `$HOME`
- `install_path`: the path where symlinks pointing to `vol.py`, `vol` and `volshell` will be created (should be in your `PATH`).
  - Default: `$HOME/.local/bin`

Example:

```sh
ansible-playbook -e venv_path='/home/me/my-venvs' -e install_path='/home/me/my-bins' -i localhost, --ask-become-pass install_volatility.yaml
```
