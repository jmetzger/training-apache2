# Training Apache2 

## Agenda 

  1. Einführung 
     * [Apache http-requests](apache-http-request.md) 
  1. Installation 
     * [Installation unter RHEL/RockyLinux](install-rhel.md)
     * [Starten/Stoppen/Aktivieren und weitere hilfreiche systemctl - Befehle](systemctl-service.md)
     * [Lauscht mein Server nach draussen](lsof.md) 
     * [Die Firewall zähmen/freischalten](firewall-cmd.md)
  1. Administration 
     * [Konfigurationsdatei mit httpd -t prüfen](httpd-t.md)
     * [Alle geladenen Module finden](script-modules.md)
     * [Mehrere Instanzen mit systemd starten](systemd-instances.md)
     * [Rechte debuggen mit der Bash für apache](rechte-debuggen-apache-user.md)
     * [Default-VirtualHost richtig konfigurieren - Achtung !](default-vhost-first.md)
     * [Alias für Fehlerseite in VirtualHost](virtualhost-error-with-alias.md)

  1. Monitoring 
     * [Status aktivieren](mod_status.md) 
  1. Rewriting / Resetting 
     * [Rewrite Header on if](if-headers.md)
     * [URL's manpulieren/umschreiben mit mod_rewrite](mod_rewrite.md)
   
  1. Performance / Optimierung 
     * [Optimierung mpm event](perf-mpm-event.md) 
   
  1. Authentication 
     * [Simple Textbased Authentication](auth-text.md)
     * [Authentication with MySQL/MariadDB](auth-mysql.md) 

  1. SSL 
     * [SSL mit letsencrypt](letsencrypt-apache.md)
     
  1. SELinux 
     * [Neuen unbekannten Port freischalten, z.B. 86](selinux-port.md)
     * [Neues DocumentRoot verwenden](selinux-new-documentroot.md)
  
  1. Absichern
     * [Standard-Apache-Seite deaktivieren (RHEL/Rocky)](disable-default-page-rhel.md)
     * [Standard-Fehlerseiten konfigurieren](default-errordocument.md)
     * [Verzeichnislisting-autoindex deaktivieren/härten](disable-autoindex.md)
     * [Keine Apache Version kommunizieren](apache-servertokens.md)
     * [Rechte härten](rechte-haerten.md)

  1. Logs 
     * [Journal persistent setzen](journal-auto.md)
  1. Tipps & Tricks 
     * [In den Root-Benutzer wechseln](sudo.md)  
     * [Wo bin ich ?](pwd.md)
     * [Nach Direktive suchen](grep.md)
     * [Praktische Ausgabe von langen Seiten - less](less.md) 
  1. Prozesse 
     * [Prozesse anzeigen - ps/pstree -p](prozesse.md)
     * [Prioritäten und NiceNess](nice-pr.md)
  1. Logs/Loganalyse
     * [Logfile beobachten](tailf.md)
     * [Dienste debuggen](debug-service.md)
     * [Journal analysieren](journalctl.md) 
  1. Dienste/Runlevel(Targets verwalten) 
     * [Die wichtigsten systemctl/service](systemctl-service.md)
  1. Hilfe 
     * [Hilfe zu Befehlen](help.md)
  1. Firewall 
     * [firewalld](firewalld.md)
     * [Scannen und Überprüfen mit telnet/nmap](nmap-telnet.md) 
  1. Netzwerk/Dienste 
     * [Hostname setzen](hostnamectl.md)
  1. Dokumentation
     * [Apache module mit Direktiven](https://httpd.apache.org/docs/2.4/en/mod/)
     * [Apache Konfigurationen (Directives) für alle Module](https://httpd.apache.org/docs/2.4/mod/directives.html)
     * [Linux Security - PDF](https://schulung.t3isp.de/documents/linux-security.pdf)



