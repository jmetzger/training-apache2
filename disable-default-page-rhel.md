# Disable Default Page 

## Walkthrough 

```
# for testing delete index.html
cd /var/www/html 
mv index.html index.html.bkup 

# 
cd /etc/httpd/conf.d 
mv welcome.conf welcome.conf.noshow # whatever suffix you like 
echo "# Disabled for security reasons" > welcome.conf 

systemctl restart httpd 
```

