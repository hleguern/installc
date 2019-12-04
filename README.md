installc
===========

# Description
Use Surfly on CentOS/RedHat 8

# Initialize server
Install basic dependencies
```bash
./preinit
```

Initialize server
```bash
ansible-playbook init.yml
```

Reboot machine
```bash
reboot
```

Configure container
- `cat node_config | lxd init --preseed`
