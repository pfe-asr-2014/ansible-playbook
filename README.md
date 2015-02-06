# Description

This playbook automates the installation of the project (except for now the Moodle server). It is designed for recent Debian/Ubuntu distributions and has been tested on Ubuntu 14.04 LTS and Ubuntu 14.10.

It provides two roles:
- learner representing what would be installed on the learner's computer
- server representing what would be installed on the central server

# Usage

Configure an inventory file like:

```
[learners]
MY_LEARNER
[learners:vars]
mooc_server_host=MY_PUBLIC_SERVER

[servers]
MY_SERVER
[servers:vars]
mooc_moodle_host=MY_MOODLE_SERVER
```

with:

- **MY_LEARNER**: the hosts you want to install the learner part on
- **MY_PUBLIC_SERVER**: the host that the learners will use to report events
- **MY_SERVER**: the hosts you want to install the server part on, can be the same as learners
- **MY_MOODLE_SERVER**: the host where your Moodle instance is installed

The most simple configuration is to use the same server, for example:

```
[learners]
192.168.1.10
[learners:vars]
mooc_server_host=192.168.1.10

[servers]
192.168.1.10
[servers:vars]
mooc_moodle_host=192.168.1.10
```

You may want to configure other variables, see `roles/learner/vars/main.yml` and `roles/learner/vars/main.yml`. You can now run the playbook:

```
ansible-playbook -i inventory_file -u root site.yml
```

You should now be able to access the overview interface on the learners's side, on port 5000, and install MOOC environnments. The server should be collecting and reporting events to your Moodle instance.
