# Docker build tools

The docker build tools will make it easy to create a docker image using Ansible.
This way, you do not have to put all the logic into the Dockerfile but can do it via Ansible.

## How does it work:

1. A docker image is created using the Dockerfile template within your project.
2. A Docker container is spun-up from this newly created image.
3. The running container is altered by executing the Ansible playbooks against this container.
4. When the playbook is finished, a final image is created from the running container.


## Installation

All tools required are within an Ansible role.<br>
To install the tools onto your laptop or CI/CD server, execute the following :

- Clone the project
```
git clone https://github.com/de-it-krachten/ansible-playbooks-docker_build.git
```
- Switch to the newly cloned repository as working directory
```
cd ansible-playbooks-docker_build
```
- Retrieve all required Ansible roles 
```
ansible-galaxy install -r roles/requirements.yml -p roles/
```
- Install all scripts & templates onto your system
```
ansible-playbook docker_build.yml -i localhost, -c local -b
```

## Initialize

- Create a new directory and make it the working directory

- Initialize that directory with templates
```
/usr/local/bin/docker-init.sh
```


- Edit all container setting in file 'docker-settings.yml'

- Edit 'Dockerfile.j2' to reflect all that you do not want or cannot do via Ansible in the next phase.

- Edit 'build-custom.yml' with any changes using Ansible

- Edit requirements.yml to include all roles your 'build-custom.yml' requires

Test image creation process by staring the build
```
/usr/local/bin/docker-build.sh
```

Final image can be push to Docker registry
```
/usr/local/bin/docker-build.sh -B -p
```
