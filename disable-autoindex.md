# Autoindex deaktivieren 

## Variante 1: Ich benötige gar keine autoindex auf dem Server 

```
# Centos / RHEL / Rocky 

# Schritt 1: 
cd /etc/httpd/conf.modules.d
# vi 00-base.conf 
# Zeile deaktivieren - Kommentar davor 
# LoadModule autoindex_module modules/mod_autoindex.so

# Schritt 2:
cd /etc/httpd/conf.d 
mv autoindex.conf autoindex.conf.noshow
# Zur Sicherheit, damit kein Update das rüberbügelt 
echo "# Disabled for security reasons" > autoindex.conf 

# Schritt 3:
systemctl restart httpd 

# Und testen wenn gewünscht 
cd /var/www/html 
mv index.html index.html.noshow
# Achtung: Welcome - Seite muss aktivieren siehe
# Siehe Menüpunkt unter Sicherheit im Inhaltsverzeichnis dieses PDF'S 
# Jetzt darf kein Index mehr kommen 
curl -I http://192.168.56.102/ 

```

## Variante 2: Ich schalte autoindex, aber will es evtl an anderer Stelle verwenden

```
# z_ deshalb, weil sie als letztes geladen werden 
# /etc/httpd/conf.d/z_security.conf 

#### Schritt 1 

# Security Measure 2
# Geht nicht, weil durch <Directory - Eintrag
# in /etc/httpd/conf/httpd.conf ueberschreiben

# Options -Indexes
# /var/www/html - spezifischer als
# /var/www/

# Ueberschreiben der Default-Seite
<Directory "/var/www/html">
    Options -Indexes
</Directory>

# Setzen fuer neue VirtualHost - Projekte
# z.B. /var/www/meine-domain.de
<Directory "/var/www">
    Options -Indexes
</Directory>

#### Schritt 2

systemctl restart httpd 

# evtl testen 
cd /var/www/html
mv index.html index.html.notused 
curl -I http://192.168.56.102  


```
