# Systemctl / Service 

## Apache starten / stoppen / aktivieren 

```
# Apache wird nach der Installation nicht standardmäßig gestartet in Centos/RHEL 
systemctl status httpd
systemctl start httpd
systemctl status httpd
systemctl is-enabled httpd
# Rückgabewert des letzten Befehls 
# Wenn nicht aktiviert kommt eine 1 raus 
echo $?

systemctl enable httpd
systemctl is-enabled httpd
# Jetzt kommt eine 0 raus 
echo $?
```

## systemctl Beispiele 
```

# Wie heisst der Dienst / welche Dienste gibt es ? (nur wenn der service aktiviert ist). 
systemctl list-units -t service 
# für apache
systemctl list-units -t service | grep ^httpd
# die Abkürzung 
systemctl -t service | grep ^httpd

# Wie finde ich einen service, der noch nicht aktiviert ist ? 
systemctl list-unit-files -t service | grep httpd

# Rebooten des Servers
# verweist auf systemctl 
reboot
systemctl reboot
shutdown -r now  

# Halt (ohne Strom ausschalten) 
halt
systemctl halt 
shutdown -h now 

# Poweroff 
poweroff
systemctl poweroff 
```

## Wie sehe ich, wie ein Service konfiguriert ist / Dienstekonfiguration anzeigen ? 

```
# z.B. für Apache2
systemctl cat apache2.service
```

## Wie kann ich rausfinden, wie die runlevel als targets heissen ?

```
cd /lib/systemd/system 
root@ubuntu2004-104:/lib/systemd/system# ls -la run*target
lrwxrwxrwx 1 root root 15 Jan  6 20:47 runlevel0.target -> poweroff.target
lrwxrwxrwx 1 root root 13 Jan  6 20:47 runlevel1.target -> rescue.target
lrwxrwxrwx 1 root root 17 Jan  6 20:47 runlevel2.target -> multi-user.target
lrwxrwxrwx 1 root root 17 Jan  6 20:47 runlevel3.target -> multi-user.target
lrwxrwxrwx 1 root root 17 Jan  6 20:47 runlevel4.target -> multi-user.target
lrwxrwxrwx 1 root root 16 Jan  6 20:47 runlevel5.target -> graphical.target
lrwxrwxrwx 1 root root 13 Jan  6 20:47 runlevel6.target -> reboot.target
```

## Welche Dienste sind aktiviert/deaktiviert 
```
systemctl list-unit-files -t service
```

## Dienste bearbeiten 
```
systemctl edit sshd.service 
# Dann eintragen
[Unit]
Description=Jochen's ssh-server 
# Dann speichern und schliessen (Editor) 

systemctl daemon-reload 
systemctl status 
```

## Targets (wechseln und default) 

```
# Default runlevel/target auslesen 
systemctl get-default 
# in target wechseln 
systemctl isolate multi-user 
# Default target setzen (nach start/reboot) 
systemctl set-default multi-user 
```

## Alle Target anzeigen in die ich reinwechseln kann (isolate) 

```
# Ubuntu 
grep -r "AllowIsolate" /lib/systemd/system 
/lib/systemd/system/reboot.target
...
...
...
systemctl isolate reboot.target 
```

## Dienste maskieren, so dass sie nicht gestartet werden können 

```
systemctl mask apache2
# kann jetzt gestartet werden
systemctl start apache2

# de-maskieren 
systemctl unmask apache2 
# kann wieder gestaret werden
systemctl start apache2
```

## systemctl Cheatsheet 

  * https://access.redhat.com/sites/default/files/attachments/12052018_systemd_6.pdf



