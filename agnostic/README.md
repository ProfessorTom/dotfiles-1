# OS Agnostic development

## Use cases

Let's say the company forces a developer to use a Windows computer, the mess of cygwin/apt-cyg and emulation posix environment doesn't satisfy you, and IT has blessed you explicitly or accidentally with vagrant and virtualbox access.

Perhaps OSX pre-installed GNU tools are too old and too much of a bother to upgrade each one using homebrew and you'd prefer running linux in a VM to develop in.

## Features

* Uses Ubuntu 18.04
* Forwards port 4000 with auto correction
* Installs vagrant-vbguest plugin for guest additions
* Installs vagrant-cachier plugin for caching packages
* Installs lightdm and xfce4 for a gui
* Installs visual studio code
* Mounts local drive to `/vagrant_data`
* Clipboard is bidirectional
* 4GB RAM, 1 vCPU, 30GB HDD

## Prerequisites

```shell
scoop install vagrant
scoop install virtualbox
```

## Setup

1. Download the `Vagrantfile`

    ```shell
    wget https://raw.githubusercontent.com/nitrocode/dotfiles/master/agnostic/Vagrantfile
    ```

1. Optionally configure the file.

    The `config.vm.synced_folder` currently mounts `C:\` to `/vagrant_data`. This would have to be changed if running in OSX/Linux.

1. Run the `vagrant` commands

    ```shell
    vagrant plugin install vagrant-vbguest
    vagrant plugin install vagrant-cachier
    vagrant up
    ```

1. If the box doesn't auto reboot after install guest additions, then run

    ```shell
    vagrant halt
    vagrant up
    ```

1. Click View > Seamless Mode (Host + L) to integrate it into your host Desktop
1. If this is a good setup, then snapshot it to save the progress.

    ```shell
    vagrant snapshot save init
    ```

    In the future, to get back to this state, use the following

    ```shell
    vagrant snapshot restore init
    ```

Note: If any of the `Vagrantfile` configurations have changed, run `vagrant reload`.
