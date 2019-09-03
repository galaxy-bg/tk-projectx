# tk-projectx
## Test assignment project

Assume that we use already deployed EC2/VM or Bare-Metal base os insatlled CentOS 7.5 and reach via SSH connections.
Based on requarments Textkernel admin user tkadmin is created manually and access to all servers v/a password also have sudo rights.

![im_name](images/tk-projectx-hld.jpg)

before start with implementing code, using common.yml we can ensure that servers are CentOS 7.5 and selinux disabled.

```
$ ansible-playbook playbooks/00-common.yml
```
## Web Server installation

inverntory file has a group webservers with three members;

[webservers]
ansible-srva
ansible-srvb
ansible-srvc

Executing command will install latest httpd service, enable firewalld allowing HTTP port and using copy module will copy 2 files index.html (customized default html file) and info.php (info.php file shows web server IP which can be used to identify server when acces via HAPorxy server IP.)

```
$ ansible-playbook playbooks/02-webservers.yml
```

## HAProxy(Loadbalancer) installation

In case one of web servers become fail or service stoped to not effect end-user experiance and access HAProxy will installed.

[loadbalancer]
ansible-lb

Executing command HAProxy enable Firewalld allowing HTTP port and HAProxy.cfg file will configured.

```
$ ansible-playbook playbooks/01-loadbalancer.yml
```
