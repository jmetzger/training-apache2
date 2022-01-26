# Default VirtualHost richtig konfigurieren (centos / rocky) 

## Wichtig !!

```
Die VirtualHost - config für den Default - Host muss immer als
erstes von Apache geparsed werden, weil der Eintrag den Default darstellt. 

Einfach realisierbar, in dem man diesen 0-default.conf nennt.

 cd /etc/httpd/sites-enabled/
[root@server1 sites-enabled]# pwd
/etc/httpd/sites-enabled
[root@server1 sites-enabled]# ls -la
insgesamt 16
drwxr-xr-x. 2 root root  95 26. Jan 13:39 .
drwxr-xr-x. 6 root root 126 26. Jan 10:11 ..
-rw-r--r--. 1 root root 177 26. Jan 10:32 00-default.conf
-rw-r--r--. 1 root root 254 26. Jan 11:46 bw.de.conf
-rw-r--r--. 1 root root 261 26. Jan 13:39 casino.bw.de.conf
-rw-r--r--. 1 root root 251 26. Jan 13:36 jobs.bw.de.conf

Default Eintrag ohne Domain, dann greift dies als Default
(Achtung: unbedingt anlegen, Server-Config greift hier nicht !!! )

# vi /etc/httpd/sites-enabled/0-default.conf 
<VirtualHost *:80>
   DocumentRoot /var/www/html
   ErrorLog ${APACHE_LOG_DIR}/default-error.log
   CustomLog ${APACHE_LOG_DIR}/default-access.log combined
</VirtualHost>

```

```
# Modifizierte httpd.service verwendet 
# damit APACHE_LOG_DIR funktioniert (standardmäßig) 
# systemctl edit httpd.service 
# schreibt override datei 
[Service]
Environment=APACHE_LOG_DIR=/var/log/httpd

systemctl restart httpd.service 

```


```
