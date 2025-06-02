# INFO

This repo is for demonstration purposes.

## Objectives

- Install and configure : Nginx, docker, HAProxy (in docker)
- Auto generate at least 2 HTML pagers from variables in Ansible
- Dynamically generate an index page that links to the other pagers
- Nginx as a web server on 2 of the VM's to serve the HTML pagers
- HAProxy configured to be a load balancer

## Assumptions

- Linux (Fedora) is installed on 3 VM's. These are the Managed nodes
- User on the node is set up with sudo permissions.
- Control node (the machine form which you run Ansible) has a ssh key pair.
- SSH public key is on Managed nodes in the ~/.ssh/authorized_keys file.

Last item Hint:

```sh
ssh-copy-id tom11w@192.168.69.4
```

## Setup

Clone this repo.

```sh
git clone git@github.com:Tom11w/ansible_demo.git
```

## Setting up Ansible

Start by setting up, activating, and installing needed packages into a python virtual environment.

```sh
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Configure Inventory

Set IP address in the `inventory.yaml` file to match the IP address's of the VM's.

## Running the Playbook

Running the following command dose a few thing:

- Tells Ansible you want to run all the plays in the file `playbook.yaml`
- `-i` is a flag to pass an 'inventory' in the next argument. Here we are passing the inventory file
- `-K` Makes Ansible ask for the SUDO password (of the user in the VM). So it can BECOME root.

```sh
ansible-playbook playbook.yaml -i inventory.yaml -K
```

After the tasks have run. The IP of the VM running HAProxy should be accessible as a website.
e.g. [http://192.168.70.3](http://192.168.70.3)

## TODO

List of things I would do if I had more time.

- Enable working with other usernames
- Access website form other computers over the network
- Automate VM creation
- Passwordless sudo
