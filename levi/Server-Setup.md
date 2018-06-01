Topic: Server security
Date: 3/21/18
***

## Basic ssh config
- Open ssh config: `vim /etc/ssh/sshd_config`
- Change from port 22
- Disable root login
- Disable empty password

## Setting up server config
- Navigate to config dir:
  - `cd /etc/nginx/sites-enabled`
- Open config file
  - ex: `sudo vim devOps`
- add domain
- add:
```javascript
location ~ /.well-known {
      allow all;
    }
```

## Install Let's Encrypt
- run `sudo apt-get update`
- run `sudo apt-get install letsencrypt`
- run `letsencrypt certonly -a webroot --renew-by-default -w /var/www/html -m levi@levibrooke.com -d c20.levibrooke.consumemorestuff.com --non-interactive --agree-tos --dry-run`

## Edit server config
- `listen 443 ssl;`
- `ssl_certificate /etc/letsencrypt/live/mysite.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/mysite.com/privkey.pem;`
- After save, run `sudo service nginx reload`

## More server config for redirect to https
- Open server config
```javascript
server {
  listen 80;

  server_name 167.99.103.99 c20.levibrooke.consumemorestuff.com;

  location ~ /.well-known {
      allow all;
  }

  location / {
      return 301 https://c20.levibrooke.consumemorestuff.com$request_uri;
  }
}
```
- After save, run `sudo service nginx reload`

## Setup Let's Encrypt renew
- sudo crontab -e
- Select vim
- "Shift G" to get to bottom of file
- "O" to insert new line
- Paste `43 6 * * * letsencrypt renew --post-hook "service nginx reload"`