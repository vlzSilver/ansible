# Collection of ansible roles

## List ansible roles

### docker-install
The role for installing Docker (https://docker.com)
> Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. Docker is also a company that promotes and evolves this technology, working in collaboration with cloud, Linux, and Windows vendors, including Microsoft.
### Role Variables
Available variables are listed below, along with default values (see `defaults/main.yml`):

    # Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
    docker_edition: 'ce'
    docker_packages:
        - "docker-{{ docker_edition }}"
        - "docker-{{ docker_edition }}-cli"
        - "containerd.io"
        - "docker-buildx-plugin"
        - "docker-compose-plugin"

The `docker_edition` should be either `ce` (Community Edition) or `ee` (Enterprise Edition). 

For remove docker use 
    ansible-playbook prod-docker.yml -t docker-node-clean