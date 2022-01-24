# Firewall aktivieren für httpd 

## Short: Aktivieren 

```
firewall-cmd --add-service=http 
firewall-cmd --runtime-to-permanent 

# oder 
firewall-cmd --add-service=http --permanent 
firewall-cmd --reload 
```
## Long version 

```
systemctl status firewalld
man firewall-cmd
firewall-cmd --state
firewall-cmd --get-zones
firewall-cmd --get-active-zones
# alle einstellungen der public zone 
firewall-cmd --list-all

# Welche Services gibt es ? 
firewall-cmd --get-services

# Services  des Distributors 
ls -la /usr/lib/firewalld/services 
cat /usr/lib/firewalld/services/http.xml

# Aktuelle abgespeicherte Konfiguration (permanent)
cat /etc/firewalld/zones/public.html 

# Welches Backend wird verwendet 
cat /etc/firewalld/firewalld.conf | grep -i Backend

```
