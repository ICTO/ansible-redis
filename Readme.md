# Readme

## Description

*ansible-redis* is an [Ansible](http://ansible.cc) playbook.
The playbook contains tasks to install Redis server, with optionally the Redmon dashboard.

## Requirements

### Ansible

Everything is documented on the [Ansible](http://ansible.cc/docs/gettingstarted.html) site...

### Supported platforms

Playbook tested on *Debian-7.0-b4-amd64*, probably works on other Debian versions too. Heavily depends on *apt*, sorry CentOS users...

## Usage

### Get the code

```bash
$ git clone git@github.ugent.be:tberton/ansible-redis.git
```

### Create a host file

Following example make ansible aware of the Vagrant box reachable on localhost port 2222.

```bash
$ vi ansible.host
```

with

```
[vagrant]
127.0.0.1 ansible_ssh_port=2222
```

### Create host specific variables

Make the host_vars directory where *ansible.host* file is located.

```bash
$ mkdir host_vars
```

Create a file in the newly created directory matching your host.

```bash
$ cd host_vars
$ vi 127.0.0.1
```

with

```
---
with_redmon: true
```

### Example output

```
SSH password: 

PLAY [vagrant] ********************* 

GATHERING FACTS ********************* 
ok: [127.0.0.1]

TASK: [Install Redis server: redis-server] ********************* 
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
127.0.0.1                   : ok=8    changed=2    unreachable=0    failed=0    
```

### Run the playbook

Use *ansible.host* as inventory. Run the playbook only for the remote host *vagrant*. Use *vagrant* as the SSH user to connect to the remote host. *-k* enables the SSH password prompt.

```bash
$ ansible-playbook -k -i ansible.host ansible-redis/setup.yml --extra-vars="hosts=vagrant user=vagrant"
```

## Docs and contact

Read more on the Wiki pages about how this playbook works.

http://icto.ugent.be
