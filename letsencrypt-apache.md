# Apache SSL with letsencrypt ssl 

## Step 0:

```
dnf install -y httpd 
systemctl enable httpd
systemctl start httpd 
```

## Step 1: setup virtual host 

```
# /etc/httpd/conf/httpd.conf 
IncludeOptional sites-enabled/*.conf

```

```
#  x = 1 to 7
#  apx.t3isp.de 
#  mx.t3isp.de
# mkdir /etc/httpd/sites-enabled
# cd /etc/httpd/sites-enabled 
# vi ap1.t3isp.de.conf 
<VirtualHost *:80>
    ServerName www.ap1.t3isp.de
    ServerAlias ap1.t3isp.de
    DocumentRoot /var/www/ap1.t3isp.de/html
    ErrorLog /var/log/httpd/ap1-t3isp-de-error.log
    CustomLog /var/log/httpd/ap1-t3isp-de-access.log combined
</VirtualHost>
```

```
/var/www
mkdir -p ap1.t3isp.de/html
cd ap1.t3isp.de/html/
echo "ich bin ap1 von jochen" > index.html
```

## Install certbot (Centos 8) 

```
dnf install -y epel-release 
dnf install -y certbot python3-certbot-apache mod_ssl
```

## Variant 1: Attention: virtual host - domain must be different than hostname 

```
e.g. ap1.t3isp.de (virtual host domain) != hostname 
# if this is not the case change hostname
hostnamectl set-hostname main.training.local 

# be sure to restart apache to take 
systemctl restart httpd 

```

## Variant 2: Remove <VirtualHost> </VirtualHost> - block vom ssl.conf 

```
# ssl.conf - Created by installation of mod_ssl. 
cd /etc/httpd/conf.d/
# vi ssl.conf 
remove
<VirtualHost>
....
</VirtualHost>

systemctl restart httpd 

```

## Use certbot to configure 

```
certbot --apache --register-unsafely-without-email 
```

## Test with your browser 

```
https://ap1.t3isp.de 

```

## Test Certificate with ssl labs 

  * https://ssllabs.com

## Refs:

  * https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-centos-8
