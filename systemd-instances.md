# Mehrere Instanzen mit systemd starten 

## Walkthrough 

```
### Schritt 1: Original conf kopiert
cd /etc/httpd/conf 
cp -a httpd.conf 1.conf 


### Schritt 2: Konfig anpassen 

# Zu Testzwecken nur wichtigste Konfigurationen geändert.
# In Produktion auch DocumentRoot / Logs und anderes IncludeOptional conf.d/* - Verzeichnis
# conf.modules.d koennen sie gemeinsam haben 

# Zeile mit Listen geaendert 
# von
# Listen 80
# in 
Listen 81 

# Eigenes Run Verzeichnis festlegen und eigenes PID - File 
# Load config files in the "/etc/httpd/conf.d" directory, if any.
# IncludeOptional conf.d/*.conf
DefaultRuntimeDir /run/httpd/instance-${HTTPD_INSTANCE}
PidFile /run/httpd/instance-${HTTPD_INSTANCE}.pid

# conf.d auskommentieren oder anderen Pfad (neues Verzeichnis wählen) 

### Schritt 3: Dienst starten und evtl. aktiveren 
systemctl start httpd@1.service 
systemctl enable httpd@1.service 

```




## Herleitung
```


# 
# where to find the documentation 
systemctl status httpd.service | grep Doc 
man httpd.service 
# Ausschnitt 
 To allow multiple instances of httpd to run simultaneously, a number of
       configuration directives must be changed, such as PidFile and
       DefaultRuntimeDir to pick non-conflicting paths, and Listen to choose
       different ports. The example configuration file
       /usr/share/doc/httpd/instance.conf demonstrates how to make such
       changes using HTTPD_INSTANCE variable.


# Schritt 2. instance.conf schauen 
less /usr/share/doc/httpd/instance.conf 
# und rauskopieren
DefaultRuntimeDir /run/httpd/instance-${HTTPD_INSTANCE}
PidFile /run/httpd/instance-${HTTPD_INSTANCE}.pid

# Schritt 3. /etc/httpd/conf.d/1.conf aendern 
# ans Ende anfuegen 
DefaultRuntimeDir /run/httpd/instance-${HTTPD_INSTANCE}
PidFile /run/httpd/instance-${HTTPD_INSTANCE}.pid



```
