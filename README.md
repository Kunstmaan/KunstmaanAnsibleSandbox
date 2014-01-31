Kunstmaan Bundles Standard Edition (Vagrant + Ansible)
=============================

An Ansible playbook to provision a vagrant saucy 64bit image with our latest KunstmaanBundlesStandardEdition.
Running on nginx + php5.5 (fpm) + mariadb + memcached, and you might smell a bit of hhvm...

To be continued..

## How to run this?

Install Ansible

```
sudo easy_install pip
sudo pip install ansible --quiet
```

Setup a vagrant vm
```
vagrant up --provision
```

Deploy Kunstmaan Bundles Standard Edition with a demo site
```
ansible-playbook kunstmaan/deploy.yml -i kunstmaan/hosts --private-key=$HOME/.vagrant.d/insecure_private_key
```

http://localhost:8888 at your service!
http://localhost:8888/en/admin -> admin:admin

