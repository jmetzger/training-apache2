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
## Extended Status

```
# Enabled by default in RHEL/Rocky 
# Refer to mod_status 
ExtendedStatus - "On" to track extended status information, "Off" to disable

# For Performance reasons disable it if not needed
# on possible in ServerConfiguration 
ExtendedStatus off 

```


## Ref:

  * https://httpd.apache.org/docs/2.4/mod/mod_status.html
