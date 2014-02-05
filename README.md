Kunstmaan Sandbox, using Vagrant and Ansible
=============================

Create a Kunstmaan Sandbox by simply using 4 commands:

* Install [Ansible](http://docs.ansible.com)
* Clone this repository
* Run vagrant, with provisioning
* Apply our Ansible Playbook

## Getting started

### Prerequisites
* Vagrant (>= 1.4.3)
* VirtualBox (>= 4.3*)

### Install [Ansible](http://docs.ansible.com)

```
sudo easy_install pip
sudo pip install ansible --quiet
```

### Clone this repository
```
git https://github.com/jverdeyen/KunstmaanAnsibleSandbox.git awesomeness
cd awesomeness
```
### Run vagrant, with provisioning
```
vagrant up --provision
```

### Apply our Ansible Playbook
```
ansible-playbook kunstmaan/deploy.yml -i kunstmaan/hosts --private-key=$HOME/.vagrant.d/insecure_private_key
```

### Click the following links

* [http://localhost:8888/](http://localhost:8888/app_dev.php)
* [http://localhost:8888/admin](http://localhost:8888/admin/app_dev.php)

__Login__: username: admin, password: admin

### Our setup

* Mac OS X 10.8.3
* Vagrant 1.4.3
* VirtualBox 4.3.6r91406
* ansible 1.4.4
