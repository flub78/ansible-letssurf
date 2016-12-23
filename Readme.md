Ansible scripts to setup lets-surf

requires an ansible version > 2.0 (tested on 2.2.0.0)

1) start the ansible container

  # check that the network exists
  docker network ls
  
  # create the network
  docker network create --subnet=172.18.0.0/16 mynet
  
  # start the ansible container
	docker run -d --name=ansible --net mynet --ip 172.18.0.100 -v $HOME/.ssh/id_rsa.public/:/root/.ssh/authorized_keys flub78/ansible 

2) start the ansible playbook to setup lets-surf.com

  export ANSIBLE_NOCOWS=1

  # to check that the target is reachable
  ansible -i hosts -m ping ansible

  # to launch the playbook
	ansible-playbook -i hosts -l ansible vps_init.yml
	
3) check the WEB server in the container

	http://172.18.0.100/
	

Test
----

After installation the server answer to http://www.lets-surf.comif it is a local test on a docker container, resolve the domain name in /etc/hosts
172.18.0.100    ctnr.lets-surf.com lets-surf.com www.lets-surf.com




Troubleshooting
---------------

frederic@frederic-VirtualBox ~/flub78/ansible/lets-surf $ ansible -i hosts -m ping ansible
172.18.0.100 | FAILED => SSH encountered an unknown error during the connection. We recommend you re-run the command using -vvvv, which will enable SSH debugging output to help diagnose the issue

Try direct ssh access

~/flub78/ansible/lets-surf $ docker inspect ansible

# Log on the ansible target
ssh root@172.18.0.100

Facts:
	- docker not installed on flub78. So it has never been executed from there
	- ssh access works fine using RSA key
	

