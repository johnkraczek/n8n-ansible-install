
[![DigitalOcean Referral Badge](https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg)](https://www.digitalocean.com/?refcode=0635178ae932&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

# Nodemation on DigitalOcean with Ansible
> Complete ansible playbook to provision and deploy nodemation to a Digital Ocean droplet.

## Intro
This project created to be a one step playbook to deploy new nodemation instances to [DigitalOcean](https://m.do.co/c/0635178ae932) 
using [Ansible](https://www.ansible.com/). 

I wanted to:
* Provision the droplet with a configurable admin user
* Install the required supporting software: NodeJS, N8N, Nginx, & PM2
* Manage fetching an SSL Certificate from Lets Encrypt
* Configure Nginx to pass the n8n application to the https://

## How to setup the project
You need Ansible to start with this project. [So go get it!](http://docs.ansible.com/ansible/intro_getting_started.html) I used ansible 2.9.10 for the project. 

* Clone this repo into a folder on your computer:

`git clone https://github.com/johnkraczek/n8n-ansible-install.git`

* Edit `defaults/vars.yml` with your values, Specifically update:
  * system_user:
  * email:
  * domain: 
  * N8N_BASIC_AUTH_USER: 
  * N8N_BASIC_AUTH_PASSWORD:

* Edit `hosts` and insert the IP address of your newly minted Digital Ocean Droplet (Ubuntu 20.04.3 LTS x64)
  * Don't have a Digital Ocean Acccount yet? [Get One Here](https://m.do.co/c/0635178ae932) use my link to get $100 off for the first 60 days. 
* Point the domain you added to `default/vars.yml` to the IP address you added to the `hosts` file. [Cloudflare DNS] (https://dash.cloudflare.com/) 
  Note: you will need to have cloudflare NOT proxy the domain (Orange Cloud => Grey Cloud).

## Provision the server:

`ansible-playbook main.yml`

to install all of dependancies & deploy the project on the server

## Additional Commands
Run this command to renew the certificate manually. 
The certificate renewal has been setup on a cronjob to run once every 2 months, The certificate expires every 3 months, giving you a month to fix certificate renewal issues if found.  

`ansible-playbook main.yml --tags=certificate` 