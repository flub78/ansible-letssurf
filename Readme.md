Ansible scripts to setup lets-surf

1) start the ansible container

  docker network create --subnet=172.18.0.0/16 mynet
	docker run -d --name=ansible --net mynet --ip 172.18.0.100 -v $HOME/.ssh/id_rsa.public/:/root/.ssh/authorized_keys ansible 

2) start the ansible playbook to setup lets-surf.com

  ansible -i hosts -m ping ansible

	ansible-playbook -i hosts vps_init.yml
	
3) check the WEB server in the container

	http://172.18.0.100/
	
	
