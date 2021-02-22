<!--

  ** DO NOT EDIT THIS FILE
  ** 
  ** This file was automatically generated by the [CLENCLI](https://github.com/awslabs/clencli)
  ** 1) Make all changes directly to YAML files: clencli/<file>.yaml
  ** 2) Run `clencli render template --name=<file>` to render this file
  **
  ** By following this practice we ensure standard and high-quality accross multiple projects.
  ** DO NOT EDIT THIS FILE

-->


![logo](https://via.placeholder.com/512x90.png)

> logo


[![GitHub issues](https://img.shields.io/github/issues/unixdaddy/do_ansible)](https://github.com/unixdaddy/do_ansible/issues)

# DigitalOcean Ansible GIT repo  ( 1 ) 

Used to test deploying to DigitalOcean with Ansible Engine and Tower

## Table of Contents
---




 - [Usage](#usage) 
 - [Prerequisites](#prerequisites) 
 - [Installing](#installing) 


 - [Acknowledgments](#acknowledgments) 
 - [Contributors](#contributors) 
 - [References](#references) 
 - [License](#license) 
 - [Copyright](#copyright) 


## Screenshots
---
<details open>
  <summary>Expand</summary>


| ![how-to-build](https://via.placeholder.com/512x256.png) |
|:--:| 
| *How to build* |

| ![how-to-run](https://via.placeholder.com/512x256.png) |
|:--:| 
| *How to run* |

</details>



## Usage
---
<details open>
  <summary>Expand</summary>

Run module-role playbook which will use the Ansible DigitalOcean modules that are a part of Ansible Engine - uses vault file with DigitalOcean OAUTH Token
```
$ ansible-playbook module-role.yml -i hosts --ask-vault-pass
```
The main.yml in the deploy-using-module role
```
# tasks file for roles/deploy-using-module
- name: ensure a droplet is present
  digital_ocean_droplet: <-- MODULE USED IS STANDARD ANSIBLE
    state: "{{ state }}" #present
    name: "{{ item }}" <-- NAMES FROM INVENTORY IN LOOP
    oauth_token: "{{ token }}"
    size: "{{ size }} " #s-1vcpu-1gb
    region: "{{ region }}" #lon1
    image: "{{ image }} " #ubuntu-16-04-x64
    ssh_keys: "{{ key }}" #29424620
    wait_timeout: 500
  with_inventory_hostnames:
    - server <-- USES GROUP TO BUILD VMs IN A LOOP
  register: droplet_info
- debug:
    var: droplet_info

```
Run collection-role playbook which will use the modules/plugins in the Ansible DigitalOcean collection from galaxy.ansible.com - uses vault file with DigitalOcean OAUTH Token
```
$ ansible-playbook collection-role.yml -i hosts --ask-vault-pass <---  Builds VMs with these names
```
The main.yml in the deploy-using-collection role
```
- name: ensure a droplet is present
  community.digitalocean.digital_ocean_droplet: <-- COLLECTION MODULE IS USED
    state: "{{ state }}" #present
    name: "{{ item }}" <-- NAMES FROM INVENTORY IN LOOP
    oauth_token: "{{ token }}"
    size: "{{ size }} " #s-1vcpu-1gb
    region: "{{ region }}" #lon1
    image: "{{ image }} " #ubuntu-16-04-x64
    ssh_keys: "{{ key }}" #29424620
    wait_timeout: 500
  with_inventory_hostnames:
    - server <-- USES GROUP TO BUILD VMs IN A LOOP
  register: droplet_info
- debug:
    var: droplet_info

```
The collection-tower playbook uses the same collection as collection-role.yml but small changes for use in tower. The DigitalOcean OAUTH token is stored in Tower credential and only a single VM is built

The do-deploy-k8s playbook deploys DigitalOcean droplet and then provisions the required number of K8s master and worker nodes - uses ENV variable to store DigitalOcean OAUTH Token
```
$ ansible-playbook  do-deploy-k8s.yml -i k8s-hosts <---  Builds VMs with these names
```
</details>



## Prerequisites
---
<details>
  <summary>Expand</summary>

- [Ansible Engine](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) - Configuration Management and more
- [DigitalOcean Ansible Collection](https://galaxy.ansible.com/community/digitalocean) - DigitalOcean Collection used for Ansible to interact with DigitalOcean Platform

</details>



## Installing
---
<details open>
  <summary>Expand</summary>

for Ansible - use your package manager of choice OR pip
```
$ pip install ansible
```
for DigitalOcean Collection - use requirements file ./collections/requirements.yml and ansible-galaxy command. Note: Tower will do this automatically
```
$ ansible-galaxy collection install -r ./collections/requirements.yml -p ./collections
```
</details>









## Contributors
---
<details open>
  <summary>Expand</summary>

|     Name     |         Email        |       Role      |
|:------------:|:--------------------:|:---------------:|
|  daddy, unix  |  withheld  |  learning  |

</details>



## Acknowledgments
---
<details>
  <summary>Expand</summary>

Gratitude for assistance:
  * Whocamebeforeme, All - everything


</details>



## References
---
<details open>
  <summary>Expand</summary>

  * [clencli](https://github.com/awslabs/clencli) - Cloud Engineer CLI


</details>



## License
---
This project is licensed under the Apache License 2.0.



## Copyright
---
```
Company, Inc. or its affiliates. All Rights Reserved.
```
