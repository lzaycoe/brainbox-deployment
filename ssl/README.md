# How to setup SSL certificates from Let's Encrypt

## Information

- Cloud: Azure
- OS: Ubuntu Server 20.04 LTS
- Web Server: Nginx

## Prerequisites

- Domain name:

  - You must have a domain name that you can use to generate SSL certificates.
  - You must have access to the DNS records of the domain name.

- My DNS name: `brainbox.eastasia.cloudapp.azure.com`

## Setup

- Step 1:Install `cerbot` & `nginx`:

  ```bash
  sudo apt update
  sudo apt install certbot nginx -y
  ```

- Step 2: Configure server block

  ```bash
  sudo rm /etc/nginx/sites-enabled/default
  sudo cp ./config/nginx.conf /etc/nginx/sites-available/brainbox.eastasia.cloudapp.azure.com
  ```

- Step 3: Create symbolic link to activate server block

  ```bash
  sudo ln -s /etc/nginx/sites-available/brainbox.eastasia.cloudapp.azure.com /etc/nginx/sites-enabled/
  ```

  ```bash
  sudo nginx -t
  sudo systemctl reload nginx
  ```

- Step 4: Serve ACME challenges

  ```bash
  cd /var/www
  mkdir certbot
  cd certbot
  mkdir brainbox.eastasia.cloudapp.azure.com
  ```

- Step 5: Generate SSL certificates

  ```bash
  sudo certbot certonly --webroot -w /var/www/certbot/brainbox.eastasia.cloudapp.azure.com -d brainbox.eastasia.cloudapp.azure.com
  ```

- Step 6: SSL certificates are generated in `/etc/letsencrypt/live/brainbox.eastasia.cloudapp.azure.com`

## References

- [NextJS HTTPS/SSL Made Easy](https://ryanschiang.com/nextjs-ssl-tutorial)
