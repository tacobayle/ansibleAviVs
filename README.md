# python Avi VS

## Goals
Configure a Health Monitor, Pool and VS through Ansible

## Prerequisites:
1. Make sure pip install avisdk is installed:
```
pip install avisdk==18.2.9
sudo -u ubuntu ansible-galaxy install -f avinetworks.avisdk
```
3. Make sure your Avi Controller is reachable from your ansible host
4. Make sure you have an IPAM/DNS profile configured

## Environment:

### Ansible version

```
avi@ansible:~/ansible/aviLscCloud$ ansible --version
ansible 2.9.5
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/avi/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /home/avi/.local/lib/python2.7/site-packages/ansible
  executable location = /home/avi/.local/bin/ansible
  python version = 2.7.12 (default, Oct  8 2019, 14:14:10) [GCC 5.4.0 20160609]
avi@ansible:~/ansible/aviLscCloud$
```

### Avi version

```
Avi 20.1.1
avisdk 18.2.9
```

### Avi Environment

- LSC Cloud
- VMware Cloud (Vsphere 6.7.0.42000) without NSX


## Input/Parameters:

1. Make sure you have a json file with the Avi credentials like the following:

```
avi@ansible:~/ansible/aviVs$ more vars/creds.json
{"avi_credentials": {"username": "admin", "controller": "192.168.142.135", "password": "*****", "api_version": "18.2.9"}}
avi@ansible:~/ansible/aviVs$
```

2. All the other paramaters/variables are stored in vars/params.yml
- The following parameters need to be changed:
```
avi_servers_ips:
  - 172.16.3.253
  - 172.16.3.254

avi_cloud:
  name: Default-Cloud
```

- The other varaiables don't need to be adjusted.



## Use the the ansible playbook to:
1. Create a Health Monitor
2. Create a Pool (based on the Health Monitor previously created)
3. Create a VS based on Avi IPAM (first network) and DNS (first domain name) and based on the pool previously created

## Run the playbook:
```
ansible-playbook pbAviVs.yml
```

## Improvment:
- add SE service group (to be tested)
- add log and analytics capabilities (to be tested)
- vsvip against 20.1.1 (to be tested)
