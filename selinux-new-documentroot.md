# SELinux new DocumentRoot 

```
### Schritt 1:
# neuen Ordner anlegen 
sudo su -
mkdir /htdocs
echo "testinhalt" > /htdocs/index.html

### Schritt 2:
# Zum 1. Debuggen SELinux deaktivieren
setenforce 0 

### Schritt 3:
# änderungen in config /etc/httpd/conf/httpd.conf  
DocumentRoot /htdocs
# Directoryeintrag damit Zugriff erlaubt ist 

#
# Relax access to content within /htdocs.
#
<Directory "/htdocs">
    AllowOverride None
    # Allow open access:
    Require all granted
</Directory>
#

### Schritt 4: Reload und testn 
systemctl reload httpd 
# Sollte funktionieren 
curl -I http://192.168.56.103 

### Schritt 5: SELinux aktivieren und context setzen 
setenforce 1 
semanage fcontext -a -t httpd_sys_content_t '/htdocs/.*'
restorecon -vr /htdocs

####### 2 things to consider 
# no perfect solution, because on relabeling (e.g. touch /.autorelabel and reboot)
# it will be gone 
# 1. chcon -R -t httpd_sys_content_t /htdocs/

# 2. '/htodcs/.*' is classic regex (0 or any chars = .*), 
# different to bash 
# echo .* -> show all hidden files: .* 
######

### Schritt 6: Testing
# now it works 
```
