# Clientbasierte SSL Authentifizierung 

## Walkthrough (RHEL/Rocky) 

```
mkdir -p /usr/local/src/SSL
cd /usr/local/src/SSL

# Schritt 1: ROOT-CA erstellen (firmenweit) 
openssl genrsa -out ssl.netways.de_rootca.key 4096

# Schritt 2: ROOT-CA Zertifikat erstellen  
openssl req -x509 -new -nodes -key ssl.netways.de_rootca.key -sha256 -days 3650 -out ssl.netways.de_rootca.pem

# Schritt 3: Key für Client erstellen 
openssl genrsa -out ssl.netways.de_client1.key 4096

# Schritt 4: CSR (Certificate Signing Request erstellen) 
openssl req -new -key ssl.netways.de_client1.key -out ssl.netways.de_client1.csr

# Schritt 5: Struktur für OpenSSL anlegen (default Verzeichnise, einkompiliert in openssl


```

## Where to store the ca-cert (Different on RHEL and Debian) 

  * https://stackoverflow.com/questions/37043442/how-to-add-certificate-authority-file-in-centos-7

## Refs:

  * https://www.netways.de/blog/series/ssl-leicht-gemacht/
