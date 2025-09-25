# Ansible Homeserver Setup
![Logo](https://i.imgur.com/yAyr3S2.png)

# Overview
This is made to make setting up the base system of my home server very easy

# Installation
Install arch linux ([archinstall](https://github.com/archlinux/archinstall)), log in to a non root account

- install ansible and git
    `sudo pacman -S ansible git`

- clone the repo
    `git clone TBD`

- enter the directory
    `cd homeserver`

- run the playbooks you want
    - `ansible-playbook -u $USER -K playbook_core.yml`
    - `ansible-playbook -u $USER -K playbook_zsh.yml`
    - `ansible-playbook -u $USER -K playbook_docker.yml`

yes, you write `$USER` there, which puts in the user you are logged in
the `-K` is short for `--ask-become-pass` which will prompt for password

**Removal**
After running the playbooks it be good to remove the ansible package
and bunch of its dependencies. Saves \~600MB and noise during updates.

- `sudo pacman -Rns ansible`


# Useful Commands
