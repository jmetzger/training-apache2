# Rechte debuggen apache - user 

```
[root@server1 www]# sudo su - apache -s /bin/bash

# Jetzt können wir durch die Verzeichnis wandern (mit cd)
und gucken, ob wir an die gewünschte Stelle kommen (ohne permission denied) 

cd /var/www
cd html
-bash: cd: html: Keine Berechtigung
```
