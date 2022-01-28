# Client-based SSL 

```
# In virtualHost 
SSLVerifyClient require
SSLVerifyDepth 10
SSLCACertificateFile /etc/apache2/ssl/ca.cer
```

## Zertifikat in Chrome importieren

```
chrome://settings
Klicken Sie links auf Datenschutz und Sicherheit.
Klicken Sie auf Sicherheit.
Scrollen Sie zu Erweitert.
Klicken Sie auf Zertifikate verwalten.
Suchen Sie in der Liste die neu hinzugefügten Zertifizierungsstellen
```


## Refs 

  * https://www.https-guide.de/tutorials/authentifizierung-ueber-client-zertifikate/
  * https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-on-centos-8
  * https://linuxconfig.org/apache-web-server-ssl-authentication

