# Docker-Training-NeIC2017

Connect to your VM
--------------------
```bash
ssh -i docker-tutorial.pem cloud-user@86.50.170.193
[cloud-user@docker-test ~]$ ssh -i docker-tutorial.pem cloud-user@<IP-Address>
```

Install Docker
---------------
* Install required packages:
```bash
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
* set up the stable repository:
```bash
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```
* Update the yum package index.:
```bash
$ sudo yum makecache fast
```
* Install the latest version of Docker:
```bash
sudo yum install docker-ce
```
Accept this fingerprint: 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35
