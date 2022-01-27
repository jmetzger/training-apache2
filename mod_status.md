# mod_status 

## Aktivieren 

```
# /etc/httpd/sites-enabled/00-default.conf
<Location "/server-status">
    SetHandler server-status
    Require ip 192.168.56.1
</Location>

systemctl restart httpd 
```

## Ref:

  * https://httpd.apache.org/docs/2.4/mod/mod_status.html
