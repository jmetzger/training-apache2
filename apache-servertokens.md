# Keine Apache Version kommunizieren 

```
# RHEL / Rocky 
/etc/httpd/conf.d/z_security.conf 
ServerTokens Prod 

systemctl restart httpd 

# Test 
curl -I http://192.168.56.102 

```
