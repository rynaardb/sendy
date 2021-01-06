![latest 5.1.1](https://img.shields.io/badge/latest-5.1.1-green.svg?style=flat)
![sendy 5.1.1](https://img.shields.io/badge/sendy-5.1.1-brightgreen.svg) ![php-7.4.8-apache](https://img.shields.io/badge/php-7.4.8-orange.svg) ![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

# Sendy for Docker

This is an unofficial docker image of Sendy.

<a href="https://sendy.co/?ref=kJgvA" title=""><img src="https://sendy.co/images/banners/728x90_var2.jpg" alt="Check out Sendy, a self hosted newsletter app that lets you send emails 100x cheaper via Amazon SES." width="728" height="90"/></a>

# Meet Sendy

Sendy is a self hosted email newsletter application that lets you send trackable emails via Amazon Simple Email Service (SES). This makes it possible for you to send authenticated bulk emails at an insanely low price without sacrificing deliverability.

## Main Features

- Send newsletters 100x cheaper using Amazon SES
- Beautiful reports
- White labeled client accounts
- Autoresponders
- List segmentation
- List & subscriber management
- Custom fields
- Bounce, complaint & unsubscribe handling
- Blacklist
- Custom domains
- Housekeeping
- Third party integrations & Zapier

<a href="https://sendy.co/?ref=kJgvA" title=""><img src="https://sendy.co/images/banners/125x125_var2.jpg" alt="Check out Sendy, a self hosted newsletter app that lets you send emails 100x cheaper via Amazon SES." width="125" height="125"/></a>

# Usage

## Docker

To run it:

```terminal
docker run -d --name sendy -e SENDY_FQDN=sendy.example.com -e MYSQL_HOST=sendy_db -e MYSQL_PASSWORD=superstrongpassword rynaardburger/sendy:latest
```

## Docker Compose

Using docker-compose:

```yml
version: '3.7'

services:
  # Sendy MySQL database
  db_sendy:
    hostname: sendy_db
    container_name: db_sendy
    image: mysql:5.6
    restart: always
    environment:
      - SENDY_FQDN=sendy.example.com
      - MYSQL_HOST=sendy_db
      - MYSQL_DATABASE=sendy
      - MYSQL_USER=sendy
      - MYSQL_PASSWORD=superstrongpassword
      - MYSQL_ROOT_PASSWORD=superstrongpassword
    volumes:
      - ./sendy_db:/var/lib/mysql

  # Sendy app (Sendy, PHP, Apache2)
  sendy:
    hostname: sendy_app
    container_name: sendy_app
    image: rynaardburger/sendy:latest
    restart: always
    ports:
      - 80:80
    environment:
      - SENDY_FQDN=sendy.example.com
      - MYSQL_HOST=sendy_db
      - MYSQL_DATABASE=sendy
      - MYSQL_USER=sendy
      - MYSQL_PASSWORD=superstrongpassword
    depends_on:
      - db_sendy

volumes:
  sendy_data:
```
