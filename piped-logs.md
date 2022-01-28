# Using Piped Logs 

## Example 

```
<VirtualHost *:80>
   ServerName casino.jochen.t3isp.de 
   ServerAlias www.casino.jochen.t3isp.de

   DocumentRoot /var/www/casino.bw.de/html
   ErrorLog /var/log/httpd/casino.bw.de-error.log
   CustomLog "|/usr/local/bin/logme.sh" combined
</VirtualHost>

#/usr/local/bin/logme.sh 
#!/bin/bash

while read line
do
  echo "$line" >> /var/log/httpd/somenew.log
done < "${1:-/dev/stdin}"

##### Step 3: set permissions 
chmod a+x /usr/local/bin/logme.sh 

##### Step 4: Restart 
systemctl restart httpd

```


## Refs:

  * https://httpd.apache.org/docs/2.4/logs.html#piped
