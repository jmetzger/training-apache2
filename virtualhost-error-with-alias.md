# VirtualHost error with Alias 

```
# vi /etc/httpd/sites-enabled/jobs.bw.de.conf 
<VirtualHost *:80>
   ServerName jobs.bw.de
   ServerAlias www.jobs.bw.de

   DocumentRoot /var/www/jobs.bw.de/html
   ErrorLog ${APACHE_LOG_DIR}/jobs.bw.de-error.log
   CustomLog ${APACHE_LOG_DIR}/jobs.bw.de-access.log combined
   ErrorDocument 404 /fehler
   Alias /fehler /var/www/html/404.html
   # oder direkte weiterleitung auf fehlerseite 
   # wird ein browser zurückgegeben und browser macht redirect
   # server muss domain nicht auflösen können, erst der browser 
   ErrorDocument 404 http://www.casino2.bw.de/404.html


</VirtualHost>

# 
mkdir -p /var/www/html 
echo "<html><body><h2>Personal 404</h2></body></html>" > /var/www/html/404.html 

systemctl restart httpd 

```
