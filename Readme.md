# Readme

## Description

*ansible-redis* is an [Ansible](http://ansible.cc) playbook.
The playbook contains tasks to install Redis server, with optionally the Redmon dashboard.

## Requirements

### Ansible

Everything you should know about Ansible is documented on the [Ansible](http://ansible.cc/docs/gettingstarted.html) site...

### Supported platforms

#### Debian wheezy

Playbook tested on *Debian-7.0-b4-amd64*, probably works on other Debian versions too. Heavily depends on *apt*, sorry CentOS users...

#### Ansible >= 1.0

Any Ansible version >= 1.0 should work. If not, please use the issue tracker to report any bugs.

## Usage

### Get the code

```bash
$ git clone git@github.com:ICTO/ansible-redis.git
```

### Create an Ansible inventory file

Following example makes Ansible aware of a box reachable through SSH on 127.0.0.1, port 2222.

```bash
$ vi ansible.host
```

with

```
[redis]
127.0.0.1 ansible_ssh_port=2222

[redis:vars]
with_redmon=True
```

The *ansible-redis* playbook is only executed for the host/group *redis*.

### Run the playbook

Use *ansible.host* as inventory. Run the playbook only for the remote host *redis*. Use *vagrant* as the SSH user to connect to the remote host. *-k* enables the SSH password prompt.

```bash
$ ansible-playbook -k -i ansible.host ansible-redis/setup.yml --extra-vars="user=vagrant"
```

### Example output

```
SSH password: 

PLAY [redis] ********************* 

GATHERING FACTS ********************* 
ok: [127.0.0.1]

TASK: [Install Redis server: redis-server] ********************* 
ok: [127.0.0.1]

TASK: [Bind Redis server to all interfaces] ********************* 
ok: [127.0.0.1]

TASK: [Ensure Redis server is running] ********************* 
ok: [127.0.0.1]

TASK: [Install Redmon dependencies] ********************* 
ok: [127.0.0.1] => (item=git,rubygems,g++)

TASK: [Check if bundler is installed] ********************* 
changed: [127.0.0.1] => (item=bundler)

TASK: [Install gem: bundler] ********************* 
skipping: [127.0.0.1] => (item=bundler)

TASK: [Check if redmon is installed] ********************* 
changed: [127.0.0.1] => (item=redmon)

TASK: [Install gem: redmon] ********************* 
skipping: [127.0.0.1] => (item=redmon)

TASK: [Install Redmon init script] ********************* 
ok: [127.0.0.1]

TASK: [Ensure Redis server is running] ********************* 
ok: [127.0.0.1]

PLAY RECAP ********************* 
127.0.0.1                   : ok=9    changed=2    unreachable=0    failed=0
```

## Docs and contact

Read more on the Wiki pages about how this playbook works.

http://icto.ugent.be
