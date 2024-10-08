# Collection of ansible roles

## List ansible roles

### docker-install
The role for installing Docker (https://docker.com)
> Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology, working in collaboration with cloud, Linux, and Windows vendors, including Microsoft.

Available variables are listed below, along with default values (see `defaults/main.yml`):

    # Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
    docker_edition: 'ce'

    #List of packages for install Docker
    docker_packages:
        - "docker-{{ docker_edition }}"
        - "docker-{{ docker_edition }}-cli"
        - "containerd.io"
        - "docker-buildx-plugin"
        - "docker-compose-plugin"

    #List of old docker packages to remove
    docker_old_packages:
      - docker.io
      - docker-dcc
      - docker-compose
      - docker-compose-v2
      - podman-docker
      - conainerd
      - runc

    #List of required packages before installing Docker
    docker_prerequiestes_packages:
      - curl
      - software-properties-common
      - ca-certificates
      - apt-transport-https
      - gnupg

    #URL docker repo key
    docker_key_url: https://download.docker.com/linux/ubuntu/gpg

    #Docker repo URL
    docker_repo_url: "deb https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable"

For remove Docker use:

    ansible-playbook prod-docker.yml -t docker-node-clean


### lemp
Deploy LEPM (Linux Nginx PHP-FPM Mysql) with test site and mysql connection test

Available variables are listed below, along with default values (see `defaults/main.yml`):

    lemp_install_packages:
      - nginx
      - mysql-server
      - mysql-client
      - php-fpm
      - php-mysql
      - python3-pymysql

    dest_folder

    nginx_port

    mysql_user
    mysql_pass

    nginx_site_conf_name

    test_server_site_name

For remove Docker use:

    ansible-playbook lemp.yml -t lemp-node-clean


### ufw-example
This role is example how to use UFW rule by ansible

Available variables are listed below, along with default values (see `defaults/main.yml`):

     ports_control:
       - name: tcp
         rule : allow
         number_port:
           - 80
           - 443
           - 22

       - name: udp
         rule : allow
         number_port:
           - 15699
           - 15700

       - name: tcp
         rule : deny
         number_port:
           - 5051
           - 8082

       global_rule: deny

For remove Docker use:

    ansible-playbook ufw.yml -t ufw-node-reset


### docker-lemp
Deploy LEMP with test site using docker compose

Available variables are listed below, along with default values (see `defaults/main.yml`):

     lemp_node_docker_compose: "/opt/docker" # where main compose dir
     lemp_node_docker_compose_app: "{{ lemp_node_docker_compose }}/lemp" # where lemp compose work dir
     lemp_node: "/opt/lemp" # where services working dir

     docker_service_network_name: test-lemp # docker network name for services
     docker_service_network_type: bridge # docker type network

     nginx_container_name : nginx-lemp
     php_container_name   : php-fpm-lemp
     mysql_container_name : mysql-lemp

     nginx_internal_port  : 80 # conatiner port
     nginx_external_port  : 8080 # external port

     test_site_domain_name     : "{{ ansible_hostname }}.local"

     mysql_root_password: "TestPas123#"
     mysql_default_port: 3306

     mysql_environment:
       - "MYSQL_ROOT_PASSWORD={{ mysql_root_password }}"
       - "MYSQL_TCP_PORT={{ mysql_default_port }}"

For remove Docker use:

    ansible-playbook docker-lemp.yml -t lemp-docker-node-clean
