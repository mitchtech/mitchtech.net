+++
author = "meyers"
categories = ["Tutorials"]
comments = true
date = "2015-02-13 00:58:48+00:00"
slug = "devstack-on-ec2-via-ansible"
tags = ["ansible","devstack","openstack"]
title = "Devstack on EC2 via Ansible"
banner = "http://i.imgur.com/iq37M8F.png"

+++

So you want to get an instance of OpenStack running to poke around and see what all the fuss is about without going insane. Welcome to [Devstack](http://docs.openstack.org/developer/devstack/). Once Devstack is setup you will have access to a web-based control panel with prepopulated data and instances. You will also be able to explore the OpenStack API with v2.0 and v3 authentication (keystone).

![devstack webpanel](http://i.imgur.com/iq37M8F.png)

### Setup

```
git clone https://github.com/chrismeyersfsu/playbook-devstack
cd playbook-devstack/
sudo ansible-galaxy install -r requirements.yml
```

* Create an ec2 elastic ip address and override the playbook variable `ec2_elastic_ip`.
* Map a domain/subdomain in route53 (or other dns service) to your elasic ip address. (i.e. devstack.example.com)
* Set your webportal login password by overriding the playbook variable `nova_password`

### Execution
Be aware that the playbook may take > 20 minutes on an ec2 instance to complete.

```
ansible-playbook site.yml -i 'devstack.example.com,'
```

When finished you should be able to visit [http://devstack.example.com](http://devstack.example.com) and login using demo / `nova_password`. You should then see the webpanel similar to the image above. The v2.0 and v3 APIs are accessabile via [http://devstack.example.com:5000/v2.0/](http://devstack.example.com:5000/v2.0/) and [http://devstack.example.com:5000/v3/](http://devstack.example.com:5000/v3/).

### Debugging
So things maybe didn't go according to plan. Here are some playbook invocation variations that you can be used to execute a subset of the tasks.

* Do not provision a new ec2 instance. Only run the devstack install task.

```
ansible-playbook site.yml -i 'devstack.testing.ansible.com,' -vvvv --tags "devstack_setup"
```

* Do not provision a new ec2 instance nor run the devstack install task. Only run the vm instance creation tasks.

```
ansible-playbook site.yml -i 'devstack.testing.ansible.com,' -vvvv --tags "devstack_nova"
```
