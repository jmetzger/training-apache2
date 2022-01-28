# Authentication (using files) 

## Example config 

```
# Ubuntu / Debian 

htpasswd -c /etc/apache2/.htpasswd kurs 
htpasswd /etc/apache2/.htpasswd another_user

# RHEL / Rocky  - password 
htpasswd -c /etc/httpd/.htpasswd kurs 
htpasswd /etc/httpd/.htpasswd another_user

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog /var/log/httpd/error.log
    CustomLog /var/log/httpd/access.log combined

    <Directory "/var/www/bw.de/html/private/">
        AuthType Basic
        AuthName "Bitte Einloggen:"
        AuthUserFile /etc/httpd/.htpasswd 
        # AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>
</VirtualHost>
```



## Ref:

  * https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-apache-on-ubuntu-14-04
