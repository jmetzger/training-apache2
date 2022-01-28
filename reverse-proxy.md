# Reverse Proxy on Rocky/RHEL 

## Einfacher Proxy 

```
# auf balancer 
ProxyPass / http://10.135.0.9 
ProxyPassReverse / http://10.135.0.9
# Braucht der Proxy den Hosteintrag oder nicht ? 
# Default deaktiviert und in der Regel nicht benötigt 
# ProxyPreserveHost on   

systemctl restart httpd 


# Achtung bei RHEL müssen unbedingt in SELinux ausgehende 
# Verbindungen erlaubt werden
# Wenn selinux aktiviert ist -> sestatus -> enforcing 
setsebool -P httpd_can_network_connect=1

```

## Balanced. 

```

```




## Refs:

  * https://httpd.apache.org/docs/2.4/mod/mod_proxy.html#proxypreservehost
