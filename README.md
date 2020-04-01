# Modular Nginx
There are a number of other nginx roles out there including the official one but i wanted something modular that is in "my" opinion something designed moreso for Ansible and its roles.

# Usage
The role has a few sane defaults that permit most usage to get an Https server running all that is necessary is to call the role with two variables defined

```
external_DNS:  example.com
certbot_email: webadmin@example.com
```

This will register with certbot and create an nginx snipit that permits easily importing sane default SSL configurations

An example file that could be created to display a static website would be as simple as

/etc/nginx/conf.d/myhost.conf
```
server {
    listen 443 ssl;
    root         /usr/share/nginx/html;
    server_name example.com;
    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem; 

    include /etc/nginx/ssl.conf;
    
    location / {
    }


}
```

This will define example.com with the medium ssl security values from ssl-config and the http to https redirect

https://ssl-config.mozilla.org/#server=nginx&version=1.17.7&config=intermediate&openssl=1.1.1d&guideline=5.4

# Advanced

There are numerous other options within the [defaults/main.yml](./defaults/main.yml) that can change other parts of the behavior of the system