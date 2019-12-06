installc
===========

# Description
Install Surfly on CentOS/RedHat 8

# Server requirements
 - CentOS/RedHat 8
 - 4 core 2.5 GHz CPU
 - 8 GB RAM
 - 60 GB Disk space
 - 100Mbps network connection

# Installation
- Make sure that the user on the system is able to run commands with sudo without providing the password:
  - Add user to the wheel group
    ```bash
    dnf install sudo
    usermod -a -G wheel <username>
    ```
  - Create file `/etc/sudoers.d/surfly` with the following content
    ```bash
    <username> ALL = NOPASSWD : ALL
    ```

- Clone installation script to the server
  ```bash
  sudo dnf install git
  git clone https://github.com/surfly/installc.git
  ```

- Initialize server
  - Install basic dependencies
    ```bash
    ./preinit
    ```

  - Initialize container manager
    ```bash
    ansible-playbook init.yml
    ```

  - Reboot machine

  - Configure container
    ```bash
    ./postinit
    ```

  - Restart container
    ```bash
    lxc restart <container_name>
    ```

- Install Surfly
  ```bash
  ./setupc
  ```
  > The very first time you run `./setupc` command, it generates `config.yaml` file which contains a default Surfly configuration.
  Every time `./setupc` command is executed, `config.yaml` file is pushed inside the container and used to install/update
  Surfly.

  > Check `certificates` configuration option [here](https://docs.surfly.com/installation/#configuration) to configure Surfly to use correct certificates and use the command below to transfer certificates to the container

# Usage
> You can check the name of the Surfly container in `installc/.container_name` file or by running `lxc list` command

Surfly configuration is located in `installc/config.yaml`. Please check all available configuration option [here](https://docs.surfly.com/installation/#configuration)

## How to transfer files inside the container?
```bash
lxc file push <file> <container_name>/home/client/install/
```
where `<file>` is the path to the file on the host machine, `<container_name>` is the name of the Surfly container

## How to log in to the Surfly container?
```bash
lxc exec <container_name> -- sudo --login --user client
```

## How to update Surfly?
Navigate to installc directory and run
```bash
./setupc
```
