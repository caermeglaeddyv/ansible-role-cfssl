Ansible role: CFSSL
=========

This role is used to generate cfssl profiles and certificates.

For now, it does the following:
- generates cfssl root CA and server certificates


Requirements
------------

This is not strict requirements and it may not work with other versions than tested ones.
Anyway. feel free to test by yourself, suggest addition of new functionality and contribute.

Role is tested with:
- Ansible version >= 2.8.6

cfssl and cfssljson must be installed on localhost if cfssl_create variable is set to True (default).


Role Variables
--------------

Variables and their descriptions copied from defaults/main.yml

```bash

# Variable which is common for most projects, used in
# configuration files or file/directory names.
# By default used as reference for cfssl_project_dir variable:
cfssl_project_name: test

# Variable which is common for most projects, used as
# project working directory on the localhost for the role.
# Currently is used to store created certificates:
cfssl_project_dir: "{{ cfssl_project_name }}"

# Common name for Root CA:
cfssl_ca_cn: "cfssl root ca"

# Key algorithm for Root CA:
cfssl_ca_key_algo: "rsa"

# Key size for Root CA:
cfssl_ca_key_size: 4096

# Distinguished names for Root CA:
cfssl_ca_names:
- c: "Neverland"
  l: "Rivia"
  o: "Witchers"
  ou: "Caer Morhen"

# server certificate expiry in hours:
cfssl_server_expiry: "17520h"

# certificate usage types:
cfssl_server_usages:
- digital signature
- key encipherment
- server auth

# Common name for server certificate:
cfssl_server_cn: "server"

# Key algorithm for server certificate:
cfssl_server_key_algo: "rsa"

# Key size for server certificate:
cfssl_server_key_size: 2048

# Distinguished names for server certificate:
cfssl_server_names:
- c: "Neverland"
  l: "Rivia"
  o: "Witchers"
  ou: "Caer Morhen"

# Hostnames, DNS names and/or IP addressed for which
# server certificate will be signed. If your server hostnames
# and IP addresses are different from ones in inventory,
# provide them manually using this variable:
cfssl_server_hosts: []

# Prefix that will be added to each generated file name:
cfssl_prefix: test

```


Dependencies
------------

cfssl and cfssljson must be installed on localhost if cfssl_create variable is set to True (default).


Example Playbook
----------------

```bash
---
- hosts: localhost
  gather_facts: false
  become: no
  tasks:
  - name: Check ansible version >=2.8.6
    assert:
      msg: Ansible must be v2.8.6 or higher
      that:
      - ansible_version.string is version("2.8.6", ">=")
    tags:
    - check
  vars:
    ansible_connection: local

- hosts: all
  become: yes
  tasks:
  - import_role:
      name: cfssl

```

More detailed examples ( inventories, playbooks etc. ) of this and other roles can be found [here](https://github.com/caermeglaeddyv/examples/tree/dev/ansible).

It's highly recommended to start you test deploys from there, especially if you use Google Cloud Platform or VMware vCenter as your infrastructure, for now that [repository](https://github.com/caermeglaeddyv/examples) contains [Packer](https://github.com/caermeglaeddyv/examples/tree/dev/packer) and [Terraform](https://github.com/caermeglaeddyv/examples/tree/dev/terraform) examples to build templates and deploy machines on this platforms.


License
-------

[Apache 2.0](https://github.com/caermeglaeddyv/ansible-role-cfssl/blob/dev/LICENSE)


Author Information
------------------

Copyright 2020 [caermeglaeddyv](https://github.com/caermeglaeddyv)
