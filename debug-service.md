# Debug Service 

## Walkthrough 

```
# Dienst startet nicht / nach Ausführen von systemctl restart wird Fehlermeldung ausgegeben
systemctl restart httpd

# Schritt 1 : status -> was sagen die logs (letzte 10 Zeilen) 
systemctl status httpd

# Nicht fündig-> Schritt 2:
jourrnalctl -xe

# Nicht fündig -> Schritt 3:
journalctl -u httpd.service 

# Nicht fündig -> Schritt 4:
# Spezifisches Log von Dienst suchen 
# und evtl. LogLevel von Dienst hochsetzen
# z.B. bei mariadb (durch Internetrecherche herausfinden) 
less /var/log/httpd/error_log 

# Nicht fündig -> Schritt 5
# Allgemeines Log
# Debian/Ubuntu 
/var/log/syslog
# REdhat/Centos 
/var/log/messages 
```

## Find error in logs quickly

```
cd /var/log/httpd 
# -i = case insensitive // egal ob gross- oder kleingeschrieben
cat error_log | grep -i error
```

