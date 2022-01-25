# Standard Error-Documents einrichten 

## Warum ? 

  * Dem Angreifer so wenig wie möglich Informationen geben. 
  * Prinzip: Datensparsamkeit 

## Achtung 

```
# ohne Leerzeichen in den Hochkommas funktioniert nicht
# Apache wirft einen Fehler 
ErrorDocument 404 "" 
```

## Wie ? 

```
# Variante Centos 
# z_security, damit es als letztes geladen wird und nicht 
# andere configs das auf der Serverebene überschreiben 
cd /etc/httpd/conf.d/
# vi z_security.conf 

# 400 - Bad Request 
ErrorDocument 400 " "
# 403 - Permission Denied 
ErrorDocument 403 " " 
# 404 - Not found 
ErrorDocument 404 " "
# 500 Internal Server Error 
ErrorDocument 500 " "


systemctl reload httpd 

# Try if you want 
http://192.168.56.102/somepage-which-is-not-present.html 

```
