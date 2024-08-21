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
