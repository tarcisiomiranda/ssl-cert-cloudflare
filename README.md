# Gen SSL using CERTBOT and Cloudflare API

***Install packages***
```
yum install certbot
apt install certbot
sudo snap install --classic certbot
```

```
apt -y install python3-certbot-dns-cloudflare
yum -y install python3-certbot-dns-cloudflare
pip3 install certbot-dns-cloudflare
```

***Create folder and secret file***
```
mkdir -p ~/.secrets/ \
&& chmod 0700 ~/.secrets/ \
&& touch ~/.secrets/cloudflare.ini \
&& chmod 0400 ~/.secrets/cloudflare.ini
```

***For multiples domains***
```
# Cloudflare API credentials used by Certbot
dns_cloudflare_email = cloudflare@example.com
dns_cloudflare_api_key = 0123456789abcdef0123456789abcdef01234
```

***OR for exclusive domain***
```
# Cloudflare API token used by Certbot
dns_cloudflare_api_token = 0123456789abcdef0123456789abcdef01234567
```

***Command for generate SSL***
```
certbot certonly \
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.secrets/cloudflare.ini \
  --dns-cloudflare-propagation-seconds 60 \
  -d example.com,*.example.com \
  -- preferred-challenges dns-0
```

***Test your SSL***
```
openssl x509 -in /etc/letsencrypt/live/YOUR-DOMAIN/fullchain.pem  -text -noout | egrep -i 'DNS:|CN'
```

