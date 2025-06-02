# INFO
This repo is demonstration purpuses.
## Objectives
- Install and config: nginx, docker, HAproxy (in docker)
- Auto generate atleas 2 HTML pagers from variables in Ansible
- Dynamicly generate an index page that links to the other pagers
- Nginx as a web server on 2 of the VM's to serve the HTML pagers
- HAproxy configured to be a load balencer

## Assumtions
- linux (fedora) is installed on 3 VM's
- set up with a user that has sudo.
- SSH access using ssh key.

Last item Hint: 
```sh
ssh-copy-id tom11w@192.168.69.4
```

# Setup
Clone this repo.
```sh
git clone git@github.com:Tom11w/ansible_demo.git
```

## Setting up Ansible
Start by setting up, activating, and installing needed packages into a python virtual enviroment.
```sh
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Configue Inventory
Set IP address in the `inventory.yaml` file to match the IP address's of the VM's.

# Running the Playbook
Running the following command dose a few thing:
- Tells ansible you want to run all the plays in the file `playbook.yaml`
- `-i` is a flag to pass an 'inventory' in the next argument. Here we are passing the inventory file
- `-K` Makes ansible ask for the SUDO password (of the user in the VM). So it can BECOME root.
```sh
ansible-playbook playbook.yaml -i inventory.yaml -K 
```

After the tasks have run. The IP of the VM running haproxy should be accessable as a website.
e.g. http://192.168.70.3



## TODO
- Enable working with other usernames
- Access form other computers
- Automate VM creation
- Passwordless sudo
