# Nodemation on DigitalOcean with Ansible
> Complete playbook to provision and deploy nodemation to a Digital Ocean droplet.

## Intro
This project created to be a one step playbook to bootstrap new projects on [DigitalOcean](digitalocean.com) 
using [Ansible](https://www.ansible.com/).

I wanted to:
* Provision the droplet with an Admin user
* Install the required supporting software: NodeJS, N8N, Nginx, & PM2
* Manage fetching an SSL Certificate from Lets Encrypt
* Configure Nginx to pass the n8n application to the https://

## How to setup the project
You need Ansible to start with this project. [So go get it](http://docs.ansible.com/ansible/intro_getting_started.html)! I used ansible 2.9.10 for the project. 

* Clone this repo into a folder on your computer:

`git clone git@bitbucket.org:funnelpress/ansible.git --depth 1 && rm -rf ./ansible/.git`

* Edit `defaults/vars.yml` with your values, Specifically update:
  * system_user:
  * email:
  * domain: 
  * N8N_BASIC_AUTH_USER: 
  * N8N_BASIC_AUTH_PASSWORD:

* Edit `hosts` and insert the IP address of your newly minted Digital Ocean Droplet (Ubuntu 20.04.3 LTS x64)
* Point the domain you added to `default/vars.yml` to the IP address you added to the `hosts` file. [Cloudflare DNS] (https://dash.cloudflare.com/) 
  Note: you will need to have cloudflare NOT proxy the domain (Orange Cloud => Grey Cloud).

## First Provision
The first step is to run 

`ansible-playbook main.yml --tags=provision`

to install all of dependancies & deploy the project on the server

## Additional Commands
Run this command to renew the certificate. 

`ansible-playbook main.yml --tags=certificate` 