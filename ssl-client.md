# Clientbasierte SSL Authentifizierung 

## Walkthrough (RHEL/Rocky) 

```
mkdir -p /usr/local/src/SSL
cd /usr/local/src/SSL

# ROOT-CA erstellen (firmenweit) 
openssl genrsa -out ssl.netways.de_rootca.key 4096

# ROOT-CA Zertifikat erstellen  
openssl req -x509 -new -nodes -key ssl.netways.de_rootca.key -sha256 -days 3650 -out ssl.netways.de_rootca.pem

```

## Where to store the ca-cert (Different on RHEL and Debian) 

  * https://stackoverflow.com/questions/37043442/how-to-add-certificate-authority-file-in-centos-7

## Refs:

  * https://www.netways.de/blog/series/ssl-leicht-gemacht/
