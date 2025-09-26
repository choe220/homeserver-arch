# Ansible Homeserver Setup
![Logo](https://i.imgur.com/yAyr3S2.png)

# Overview
This is made to make setting up the base system of my home server very easy

# Installation
Install arch linux ([archinstall](https://github.com/archlinux/archinstall)), log in to a non root account

- install ansible and git
    `sudo pacman -S ansible git`

- clone the repo
    `git clone https://github.com/choe220/homeserver-arch`

- enter the directory
    `cd homeserver`

- run the playbooks you want
- `ansible-playbook -u $USER -K playbook_core.yml`
- `ansible-playbook -u $USER -K playbook_fish.yml`
- `ansible-playbook -u $USER -K playbook_docker.yml`
- `ansible-playbook -u $USER -K playbook_zfs.yml`

yes, you write `$USER` there, which puts in the user you are logged in
the `-K` is short for `--ask-become-pass` which will prompt for password

**Removal**
After running the playbooks it be good to remove the ansible package
and bunch of its dependencies. Saves \~600MB and noise during updates.

- `sudo pacman -Rns ansible`

# ZFS
[Arch Wiki ZFS](https://wiki.archlinux.org/title/ZFS#Experimenting_with_ZFS)
After installing zfs you will need to know what disks are available. If /dev/sdb /dev/sdc /dev/sdd
- `zpool create tank raidz /dev/sdb /dev/sdc /dev/sdd`

To create the individual datasets, the command is as follows:
- `zfs create tank/{dataset name}`
---
- `zfs create tank/media`
- `zfs create tank/configs`
- `zfs create tank/docker`
- `zfs create tank/downloads`
- `zfs create tank/backups`
---

Once the datasets are created auto mounting is the next priority. There are several services that need enabled. 
- `systemctl enable --now zfs.target` - as the overarching reference point for other units to depend on
- `systemctl enable --now zfs-import.target` - as it provides the proper ordering
- `systemctl enable --now zfs-import-cache.service` - to import the pools

Export the pool to:
- `zpool set cachefile=/etc/zfs/zpool.cache tank`

# Useful Commands
|Command        |Use                        |
|       ---     |           ---             |
|`y` or `yazi`  |TUI file browser. q to quit|
|`micro`        |TUI file editor            |
|`fzf`          |Fuzzy file finder          |
|`dust`         |Storage overview           |
|`btop`         |Resource manager           |