# My Personal Ansible Collection

A set of Ansible roles to install or remove software and services on Debian and RedHat-based systems.

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Sensitive Data](#sensitive-data)
- [Roles](#roles)
- [License](#license)
- [Authors](#authors)

## Overview

This repository contains reusable roles to manage tools like Docker, Git, Java, Maven, PostgreSQL, WildFly, and Open Liberty. Some roles install native packages, others deploy apps inside containers. You can also use these roles to remove software by setting the right state.

## Project Structure
```plaintext
my-personal-ansible-collection/
├── ansible.cfg
├── inventories/
├── playbooks/
└── roles/
```


## Installation

1. Clone the repository:

```bash
git clone https://github.com/firassBenNacib/my-personal-ansible-collection.git
cd my-personal-ansible-collection

```

2. The inventory is already set in ansible.cfg.
  
3. Run a playbook:

```bash
ansible-playbook playbooks/manage_git.yml

```

## Usage

Each playbook targets one or more roles. You can change default settings (like versions or states) by editing `defaults/main.yml` in each role, or override them when running the playbook:

```bash
ansible-playbook playbooks/manage_java_maven.yml -e "java_version=21 maven_version=3.9.6"
```

To remove a package or container, set the related state variable to `absent`:

```bash
ansible-playbook playbooks/manage_docker.yml -e "docker_package_state=absent"
```

You don't need to set the inventory file manually; `ansible.cfg` handles that.

## Sensitive Data

Some roles require secrets like database credentials or WildFly admin users. These values are stored in `vars/main.yml` using Ansible Vault.

To edit them:

```bash
ansible-vault edit roles/wildfly/vars/main.yml
```

To run a playbook that uses vault-protected files:

```bash
ansible-playbook playbooks/install_wildfly.yml --ask-vault-pass
```


## Roles

- `docker`: Install or remove Docker
- `git`: Manage Git
- `java`: Install Java (supports versions like 8, 11, 17, 21)
- `maven`: Install or remove Apache Maven
- `python3`: Install Python 3 and pip
- `psql`: Install the PostgreSQL client
- `sqlplus`: Install Oracle SQL*Plus
- `wildfly`: Install and deploy Java EE apps on WildFly
- `openliberty`: Install and deploy on Open Liberty
- `prepare_ear_package`: Download and unpack EAR packages
- `oracle_docker`: Build and run Oracle 10g in a Docker container
- `postgres_docker`: Build and run PostgreSQL 16 in a Docker container
- `fix_centos_yum`: Replace broken CentOS 7 repo configs

## License

This project is licensed under the [MIT License](./LICENSE).


## Authors

Created and maintained by Firas Ben Nacib - bennacibfiras@gmail.com
