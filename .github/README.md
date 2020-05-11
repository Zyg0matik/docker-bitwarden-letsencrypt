# Docker Bitwarden running with auto generate/renew Let's Encrypt Certificate

With this repo you will be able to set up the fantastic [Bitwarden](https://bitwarden.com/) as a container over SSL auto generated and auto renewed by our Web Proxy.

![Bitwarden Enviornment](https://github.com/evertramos/images/blob/master/portainer.jpg)

# Prerequisites

In order to use this compose file (docker-compose.yml) you must have:

1. docker [https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/)
2. docker-compose [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
3. docker-compose-letsencrypt-nginx-proxy-companion [https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion](https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion)

# How to use

1. Clone this repository:

```bash
git clone https://github.com/Zyg0matik/docker-bitwarden-letsencrypt.git
```

2. Make a copy of our .env.sample and rename it to .env:

Update this file with your preferences.

```bash
#
# docker-Bitwarden-letsencrypt
# 
# Bitwarden configured to work along with our Web Proxy
# https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion
#
# This is the .env file to set up your Bitwarden enviornment

#
# Container name for your Bitwarden
#
CONTAINER_NAME=bitwarden

#
# Path where your Bitwarden files will be located
#
BITWARDEN_DATA_PATH=/path/to/your/bitwarden/data

#
# Password for Admin user
#
ADMIN_PASSWORD=your_admin_password

#
# Your domain (or domains)
#
DOMAINS=domain.com,www.domain.com,bitwarden.domain.com

#
# Main domain for SSL certificate
#
MAIN_DOMAIN=bitwarden.domain.com

#
# Your email for Let's Encrypt register
#
LETSENCRYPT_EMAIL=your_email@domain.com

#
# Path to the certificates
# If you use our webproxy should be:
# /home/user/webproxy/data/certs
BITWARDEN_SSL_PATH=/path/to/your/certs

#
# SSL Certificates previously generated
# You may use below webproxy to generate your ssl certificate
#(https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion)
#
BITWARDEN_SSL_CERTIFICATE=/certs/$MAIN_DOMAIN.crt
BITWARDEN_SSL_KEY=/certs/$MAIN_DOMAIN.key

#
# Network name
# 
# Your container app must use a network conencted to your webproxy 
# https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion
#
NETWORK=webproxy

#--
```

3. Start your container

You can run our script, and it will use your predefined password:
```bash
# ./start.sh
```

Or you can simply start your compose enviornment:
```bash
# docker-compose up -d
```

> If you run only `docker-compose up -d` you will be prompted to set your admin passowrd when accessing your browser.

> This container must be in a network connected to your webproxy containers or use the same network of the webproxy.

> Please keep in mind that when starting for the first time it may take a few moments (even a couple minutes) to get your Let's Encrypt certificates generated.

### Any further Bitwarden configuration please check [BitwardenRs Documentation](https://github.com/dani-garcia/bitwarden_rs/wiki)

