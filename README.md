The Playbook
=================
The Playbook is a collection of commonly used software for Ansible build scripts. Use this collection to quickly install software dependencies to your plays.

Debian and RedHat distros are supported, allowing users to deploy software to a variety of machines regardless of the OS family.

Installation
-----------------
Add The Playbook roles directory to your *ansible.cfg* file:
```
roles_path = /opt/playbook/roles
```

Usage
-----------------
Software dependencies can be pulled into user roles by adding a *meta/main.yml* file.
```
---
dependencies:
  - java
```
Most software installs have version numbers which can be changed. These values can be supplied as parameters to the roles as such:
```
---
dependencies:
  - { role: java, java_distro: oracle, java_version: 6 }
```
Leaving out optional parameters will install the software with the default settings.

You can add software installs directly into plays by adding them as roles.
```
---
- hosts: all
  roles:
    - java
```

Some software are installed as services. Ansible handlers are available for these services.
```
- command: /bin/true
  notify:
    - start activemq
```

Apache ActiveMQ
-----------------
#### Parameters
- *activemq_version* Version of ActiveMQ to install. Default 5.10.0
- *activemq_folder* Absolute path to directory where ActiveMQ will be installed. Default /opt

#### Service
ActiveMQ is installed as a `activemq` service. Handler is defined as `activemq`. Supported functions:
- start
- stop
- restart

Apache HTTP Server
------------------
#### Parameters
none
#### Service
Apache is installed as `apache2` service on Debian and `httpd` on RedHat. Handler is defined as `apache`. Supported functions:
- start
- stop
- restart

Build Tools
-----------------
#### Parameters
none

cURL
-----------------
#### Parameters
none

EPEL for YUM
-----------------
Adds the EPEL repository to yum on RedHat machines.
#### Parameters
none

Gearman
-----------------
#### Parameters
none

Git
-----------------
#### Parameters
none

Java
-----------------
#### Parameters
- *java_distro* Either openjdk or oracle. Default openjdk
- *java_version* Version 6 or 7 for openjdk. Version 6, 7 or 8 for oracle. Default 7

At the moment, Oracle Java installs are not supported by The Playbook for RedHat machines.

NTP Daemon
-----------------
#### Parameters
none
#### Service
NTP daemon is installed as `ntp` service on Debian and `ntpd` on RedHat. Handler is defined as `ntp`. Supported functions:
- start
- stop
- restart

Ruby
-----------------
Rubies installed are available only for the current user.
#### Parameters
- *ruby_version* Version of Ruby to install. Version format follows the `rvm install` command.

ZeroMQ
-----------------
#### Parameters
- *zeromq_version* Version of ZeroMQ to install. Default 4.0.4
- *zeromq_folder* Absolute path to directory where ZeroMQ will be installed. Default /opt
