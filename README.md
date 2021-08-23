# Houses Playbook

This is an ansible playbook to help you get up and running with <a href = "https://github.com/ryandt33/the-house-system">The House System</a>.

This is setup to work on <i>Ubuntu 20.04</i>, with other distros YMMV.

Secondly, it is designed to install on the localhost, however, you can edit the configuration for remote installation easily.

## Installation

On a fresh Ubuntu installation, update your system.

```
sudo apt update && sudo apt upgrade
```

Install git and ansible.

```
sudo apt install git ansible
```

As well as the ansible community libraries

```
sudo ansible-galaxy collection install community.general
```

Then clone into this repo and move into the directory.

```
git clone https://github.com/ryandt33/house-playbook.git && cd house-playbook
```

## Configuration

Setup your school details in the /houses.yaml file

```
  vars:
    #variable needed during node installation
    var_node: /tmp #You can leave this alone
    ansible_dir: /home/{your-user-id}/house-playbook #change this to where you cloned the repo
    install_dir: /home/{your-user-id}/the-house-system #this is your installation directory
    site_name: houses.example.com #this is where people will access your website
    api_name: house-api.example.com #this is the server for your api
```

Set your house system details in /default.json

```
{
  "mongoURI": "mongodb://localhost/houses",
  "jwtSecret": "secret",
  "mbAPIKey": "123",
  "mbSuffix": "com",
  "mgURL": "api.mailgun.net/v3/{domain name}",
  "mgAPI": "321",
  "mgEmail": "myemail@mailgun.com",
  "houseURL": "https://your.house.system",
  "orgName": "Your org name",
  "useLL": false,
  "llEndPoint": "https://url/data/xAPI",
  "llHead": "Basic abcd"
}
```

## Installation

Run the following:

```
sudo ansible-playbook houses.yaml
```

## Setup certbot

Install <a href="https://certbot.eff.org/lets-encrypt/ubuntufocal-nginx.html">certbot</a> and configure SSL certificates for your domain.

```
sudo apt install snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx -d houses.example.com -d house-api.example.com
```

## Run the server

Go into your server directory.

```
cd ~/the-house-system/

npm run server-production
```

Fill out the prompts as they come up.

Close the server with CTRL+C.

Run the production server and api server.

```
npm run production
```
