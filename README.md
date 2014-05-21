Ansible Kunstmaan Sandbox
=============================

Create a Kunstmaan Sandbox by simply using 4 commands:

* Install [Ansible](http://docs.ansible.com)
* Clone this repository
* Vagrant up

## Getting started

### Prerequisites
* [VirtualBox (>= 4.3*)](https://www.virtualbox.org)
* [Vagrant (>= 1.4.3)](http://www.vagrantup.com)

### Install [Ansible](http://docs.ansible.com)

```
sudo easy_install pip
sudo pip install ansible --quiet
```

### Clone this repository
```
git clone https://github.com/Kunstmaan/KunstmaanAnsibleSandbox.git
cd KunstmaanAnsibleSandbox
```
### Run vagrant, with provisioning
```
vagrant up
```

### Click the following links

* [http://localhost:8888/](http://localhost:8888/app_dev.php)
* [http://localhost:8888/admin](http://localhost:8888/admin/app_dev.php)

__Login__: username: admin, password: admin

### Our setup

* Mac OS X 10.8.3
* Vagrant 1.4.3
* VirtualBox 4.3.6r91406
* Ansible 1.4.4
