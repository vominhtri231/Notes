# Git config

## Basic command

Set the configuration to git by:

```sh
git config [options] config-name config-value

git config --global user.name "John Doe"
```

The config values will be saved in .git/config

## Useful options

* --replace-all : replace the config with same key (default)
* --all: add a config without delete the old one
* --local: write to .git/config (default)
* --global: write to ~/.gitconfig
* --system: write to the system /etc/gitconfig

## Useful configs

1. `core.autocrlf`: should convert LF to CRLF when checking-out and vice versa:
    * true: do both
    * false: do none
    * input: only when commit
