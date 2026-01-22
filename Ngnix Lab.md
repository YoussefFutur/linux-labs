# NGINX LAB
#### This is a small documentation about usage of nginx and how to install it, manage the service and display a simple html page.

### What is XGINX ?
NGINX is a web server application with integrated reverse proxy and a load balancer.
It is light and fast, stable and can be used for large projects as well.
Its Documentation is well put out and there is a lot of free resources available, which makes it a good pro choice for web service usage.


### How to install :

More details are in the NGINX documentation for different distribution types, we will detail here the debian installation :

Installing the pre-rerequisites :
sudo apt update && \
sudo apt install curl \
                 gnupg2 \
                 ca-certificates \
                 lsb-release \
                 debian-archive-keyring

Import official nginx signing key :
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
     | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null

Verify that downloaded file contains the correct key :
gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg

Desired output :
pub   rsa4096 2024-05-29 [SC]
      8540A6F18833A80E9C1653A42FD21310B49F6B46
uid                      nginx signing key <signing-key-2@nginx.com>

pub   rsa2048 2011-08-19 [SC] [expires: 2027-05-24]
      573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
uid                      nginx signing key <signing-key@nginx.com>

pub   rsa4096 2024-05-29 [SC]
      9E9BE90EACBCDE69FE9B204CBCDCD8A38D88A2B3
uid                      nginx signing key <signing-key-3@nginx.com>

If these fingerprints do not match, detete the file immediately

Setup the apt respository (stable) :
echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
https://nginx.org/packages/debian `lsb_release -cs` nginx" \
    | sudo tee /etc/apt/sources.list.d/nginx.list

Install the nginx package :
sudo apt update && \
sudo apt install nginx

Startup nginx, and verify that its up and runing using the curl command :
curl -I 127.0.0.1

Desired output :
HTTP/1.1 200 OK
Server: nginx/1.29.3


### Where is NGNIX ?

Binairies : /usr/sbin/nginx
Main configuration : /etc/nginx/nginx.conf
Sites : /etc/nginx/sites-available/
Active Sites : /etc/nginx/sites-enabled/
Logs : 
  access : /var/logs/nginx/access.log
  error : /var/log/nginx/error.log

### Manage the service

sudo systemctl -start -status -stop -restart nginx , chose the desired option

'sudo systemctl enable nginx' to have nginx launch at startup


### Create a simple html page :

modify : 
sudo nano /var/www/html/index.html

Example content :

<!DOCTYPE html>
<html>
  <head>
    <title>My cool page</title>
  </head>
  <body>
    <h1>NGINX is working</h1>
    <p>Installed on my Linux VM</p>
  </body>
</html>


