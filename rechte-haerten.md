# Rechte haerten 

```
# RHEL / Rocky 
cd /var/www
chown -R apache:apache html 
# Ausführungsrechte nur für Verzeichnisse,
# keine Ausführsrechte für Dateien (erreicht mit X)
chmod -R u-x,g-x,u=rwX,g=rwX,o= daten

```
