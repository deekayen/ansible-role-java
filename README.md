java
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-java.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-java)

Provides java (oracle or openjdk), jre or jdk, versions 6, 7, 8 or 9 for many distributions:
- Alpine
- CentOS
- Debian
- Fedora
- Ubuntu

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/robertdebock.github.io/artifacts/java.png "Dependency")

Requirements
------------

- For openjdk: Access to a repository containing packages, likely on the internet.
- For oracle: Download the rpms and/or tar.gz's from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and place then in the "files" directory. These files are not included because a license has to be accepted. For each version download the "jre" and "jdk", x64 version.

Role Variables
--------------

- java_version: 6, 7, 8, 9 or 10, defaults: 8
- java_vendor: openjdk or oracle, default: openjdk
- java_type: jdk or jre, default: jre
- java_format: rpm or targz, default: targz. (only applicable for java_vendor: oracle)
- java_install_directory: for targz installations, default: /opt. (only applicable for java_vendor: oracle)
- java_jce: "yes" if you want to install the Java Cryptography Extension, default: unset (only applicable for java_vendor: oracle and java_version: 8)

Have a look in vars/main.yml to see all available combinations.

Dependencies
------------

You can prepare your system using this role:

- robertdebock.bootstrap

Download all dependencies by issuing this command:
```
ansible-galaxy install -r requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-3.6|yes|yes|yes|
|alpine-3.7|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|yes|yes|yes|
|centos-7|yes|yes|yes|
|debian-buster|yes|yes|yes|
|debian-stretch|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-27|yes|yes|yes|
|fedora-28|yes|yes|yes|
|opensuse-42.2|yes|yes|yes|
|opensuse-42.3|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-bionic|yes|yes|yes|

Example Playbooks
----------------

For a default installation (defaults in defaults/main.yml) use this playbook:
```
- hosts: servers
  gather_facts: yes
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.java
```

For an installation of Oracle jdk version 9, use this playbook:
```
- hosts: servers
  gather_facts: yes
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.java
      java_vendor: oracle
      java_type: jdk
      java_version: 9
      java_format: rpm
```

Red Hat distributes Oracle Java, so this may be an appropriate playbook:
```
- hosts: all
  gather_facts: yes
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.java
      java_vendor: oracle
      java_format: rpm
      java_rpm_source: repository
```

Install this role using `galaxy install robertdebock.java`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock <robert@meinit.nl>
