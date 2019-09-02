# tk-projectx
Test assignment project

The purpose of this project is using Ansible deploy and/or re-deploy multiple web instance(s) without effecting end-user experiance providing high availability.

Assume that we use already deployed EC2/VM or Bare-Metal base os insatlled CentOS 7.5 and reach via SSH connections.

![im_name](images/tk-projectx-hld.jpg)

Web Server installation

inverntory file has a group webservers with two members;

[webservers]
ansible-srva
ansible-srvb

Executing command will install latest httpd service, enable firewalld allowing HTTP port and using copy module will copy 2 files index.html (customized default html file) and info.php (info.php file shows web server IP which can be used to identify server when acces via HAPorxy server IP.)

$ ansible-playbook playbooks/02-webservers.yml

HAProxy(Loadbalancer) installation

In case one of web servers become fail or service stoped to not effect end-user experiance and access HAProxy will installed.

[loadbalancer]
ansible-lb

Executing command HAProxy enable Firewalld allowing HTTP port and HAProxy.cfg file will configured.

$ ansible-playbook playbooks/01-loadbalancer.yml

