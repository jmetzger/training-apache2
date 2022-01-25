# SELinux - port freischalten (unbekannter Port) 

## Walkthrough (kurzer Weg) 

```
/etc/httpd/conf.d/httpd.conf 
# Weiteren port eintrag 
Listen 86 

systemctl restart httpd 
# serer startet nicht 

semanage port -a -t http_port_t  -p tcp 86
systemctl start httpd.service

```

## Walkthrough Lösung - lange Form 

```
/etc/httpd/conf.d/httpd.conf 
# Weiteren port eintrag 
Listen 86 

systemctl restart httpd 
# serer startet nicht 

# sealert muss installiert sein, wenn nicht
dnf whatprovides sealert 
# paket installieren 

cd /var/log/audit 
sealert -a audit.log > report.txt

#.In der Report finden wir auch semanage anweisungen 


# In welcher Kategorie (Port-Kategorie) soll der Port hinzugefügt werden
# Maßgeblich ist die Zeile, in der 80,81 etc vorkommt 
semanage port -l | grep 80 
# http_port_t 


```

## In welchem Kontext läuft der Apache-Server 

```
ps auxZ | grep httpd 
..... :httpd_t:s0 

```
