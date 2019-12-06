installc
===========

# Description
Use Surfly on CentOS/RedHat 8

# Initialize server
- Install basic dependencies
  ```bash
  ./preinit
  ```

- Initialize server - install lxd
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

- Run Surfly installation
  ```bash
  ./setupc
  ```
