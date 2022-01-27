# Authentication (using files) 

## Example config 

```
htpasswd -c /etc/apache2/.htpasswd sammy
htpasswd /etc/apache2/.htpasswd another_user


<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog /var/log/httpd/error.log
    CustomLog /var/log/httpd/access.log combined

    <Directory "/var/www/html">
        AuthType Basic
        AuthName "Restricted Content"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    </Directory>
</VirtualHost>
```



## Ref:

  * https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-apache-on-ubuntu-14-04
