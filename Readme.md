# Readme

## Description

*ansible-redis* is an [Ansible](http://ansible.cc) role.
The role contains tasks to install Redis server, with optionally the Redmon dashboard.

## Provides

1. Redis
2. Redmon dashboard

## Requires

1. Ansible 1.4 or higher
2. Debian 7.3 (other deb-based distros should work too)
3. Vagrant (optional)

## Usage

### Get the code

```bash
$ git clone git@github.com:ICTO/ansible-redis.git
```

### Create the playbook file

```
---
- name: Redis
  hosts: redis
  roles:
    - ansible-redis
```

### Run the playbook

Use *ansible.host* as inventory. Run the playbook only for the remote host *redis*. Use *vagrant* as the SSH user to connect to the remote host. *-k* enables the SSH password prompt.

```bash
$ ansible-playbook -k -i ansible.host redis.yml -u vagrant
```

### Example output

```
SSH password: 

PLAY [Redis] ****************************************************************** 

GATHERING FACTS *************************************************************** 
ok: [127.0.0.1]

TASK: [ansible-redis | Install Redis server] ********************************** 
ok: [127.0.0.1]

TASK: [ansible-redis | Bind Redis server to all interfaces] ******************* 
ok: [127.0.0.1]

TASK: [ansible-redis | Ensure Redis server is running] ************************ 
ok: [127.0.0.1]

TASK: [ansible-redis | Install Redmon dependencies] *************************** 
ok: [127.0.0.1] => (item=git)
ok: [127.0.0.1] => (item=ruby1.9.1)
ok: [127.0.0.1] => (item=ruby1.9.1-dev)
ok: [127.0.0.1] => (item=g++)

TASK: [ansible-redis | Install Redmon gems] *********************************** 
ok: [127.0.0.1] => (item=bundler)
ok: [127.0.0.1] => (item=redmon)

TASK: [ansible-redis | Install Redmon init script] **************************** 
ok: [127.0.0.1]

TASK: [ansible-redis | Ensure Redis server is running] ************************ 
ok: [127.0.0.1]

PLAY RECAP ******************************************************************** 
127.0.0.1                  : ok=8    changed=0    unreachable=0    failed=0   
```
