# Setup Ubuntu

### Table of Contents

- [Update Packages](#update-packages)
- [Customization](#customization)
- [Git Alias](#git-alias)

## Update Packages

We run the project on Ubuntu 22.04 and use Python3.10 for this project. Update
the system packages and install essential packages with the command lines below.

```bash
sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential
```

The command line above also installs Makefile for running and compiling your
programs more efficiently automation.

## Customization

You can add Bash customizations to display Git branch in your terminal. Open
your file `~/.bashrc` and add the following to the bottom of the file.

```bash
# ********** BASH CUSTOMIZATIONS **********

# Configure terminal prompt.
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PS1='\[\e[0;32m\]\u@\h\[\e[m\] \[\e[1;36m\]\w\[\e[1;33m\] $(parse_git_branch)\[\e[m\] \[\e[1;32m\]\n$\[\e[m\] \[\e[1;37m\]'
export CLICOLOR=1
export LSCOLORS=gxfxcxdxbxegedabagacad
```

## Git Alias

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.cp cherry-pick
```

## Clean Up Disk

To find out how big your your apt cache is, run:

```bash
du -sh /var/cache/apt/archives
```

Clean the apt cache on Ubuntu using the command:

```bash
sudo apt-get clean
```
