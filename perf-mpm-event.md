# Performance - Optimierung (mpm-event) 

## Ziel

  * mehr Anfragen pro Sekunden(Requests/Sec) 
  * Stabiles System 

## Grundberechnung (Variante 1) 

   * Aapche und php-fpm 

```
Estimating Thrashing (Prügel) - Point 
(hier fängt er an auszulagern) 

free -h 
( total memory - buffer/cache - Reserved ) / Average Apache

Wie ist es mit php:
5 Kind-Prozesse,pro Prozess (pool): 18,5 MB 


Beispielrechnung:

Schritt1: Speicher für Apache ermitteln 

  800MB Arbeitsspeicher 
- 308MB buffer/cache Betriebssystem 
===================================
  492MB Speicher für alle Dienste zu vergeben 
- 100MB für 5 Prozesse php-fpm 
===================================
- 400MB für Apache 

Schritt2: Wieviel Kind-Prozesse sind möglich 

1. Miniscrhitt: Ermittlung der durchschnittlichen 
Größe eines Apache - Prozesses: rund 16,5 MB = grosszügig 20 MB 

2. Minischritt: Wieviel Kind/Child-Prozesse möglich 
400MB / 20 MB = Anzahl MÖGLICHE Kindprozesse 
= ca 20 

3. Aus Spaß Threads: 
25 Threads pro Prozess: 500 Threads  

```

## Ausgewogenheitsberechnung 

```
pro Kind Prozess von Apache (Standard) 25 Threads 
d.h. aktuell 100 Threads 

demgegenüber 5 Prozesse php 
d.h. hoch ziehen auf 100 
d.h. 100 * 18 MB = 1,8 GB 

d.h. unter 3 GB Arbeitsspeicher (1GB vorhanden aktuell)
brauchen wir hier garnicht anfangen 

```

## Grundberechnung (Variante 2) 

  * Apache und vielleicht noch einen kleinen Dienst (undefiniert)

```

Beispielrechnung:

Schritt1: Speicher für Apache ermitteln 

 2000MB Arbeitsspeicher 
- 308MB buffer/cache Betriebssystem 
===================================
 1892MB Speicher für alle Dienste zu vergeben 
- 500MB 25% Pauschal für andere Prozesse  
===================================
-1392MB für Apache 

Schritt2: Wieviel Kind-Prozesse sind möglich 

1. Miniscrhitt: Ermittlung der durchschnittlichen 
Größe eines Apache - Prozesses: rund 16,5 MB = grosszügig 20 MB 

2. Minischritt: Wieviel Kind/Child-Prozesse möglich 
1300MB / 20 MB = Anzahl MÖGLICHE Kindprozesse 
= 60 Apache prozesse 

3. Aus Spaß Threads: 
25 Threads pro Prozess: 1500 Threads  

```

## Sind soviele Threads hilfreich ? 

```
# Was sind begrenzende Faktoren (bottleneck) (nur Apache) ?
o i/o = schreiben und lesen auf und von Platte
o CPU (wie schnell CPU und wiele Operation können gleichzeitig
  verarbeiten)

# Was sind Testschritte.
1. System unter Last setzen (ab - apache benchmark -c (gleichzetigie Prozesse -n wieviele Abfragen)

# Wie sehe ich, ob das Sinne soviele Threads zu haben. 
top 

```

## CPU gebundene Last erkennen und handeln 

```
# Habe ich einen io-gebunden oder cpu-gebundene Last
# CPU-gebundene Last 
# Was heisst das ?
Die CPU pfeift das aus dem letzten Loch 
Auch, wenn ich eine schnellere Platte habe, 
nützt das nix, weil die zu langsame CPU der begrenzende 
Faktor ist 

# Wie finde ich das heraus ?
top
1) In der Übersicht: CPus: us und u.U. sy wert Hoch 
2) load average hoch:
Spalte 1: Wieviele Prozesse warteten im Durchrschnitt auf Ausführung durch die CPU in der letzten Minute
Spalte 2: Das gleiche wie 1 nur in den letzten 5 Minuten 
Spalte 3: Das gleiche wie 1 nur in den letzten 15 Minuten
3) In CPU-Zeile: wa-wert ist 0 oder niedrig. 

# Was tun ? 
A) Schnellere CPU kaufen (horizontal skalieren) 
oder
B) Weitere Systeme zu Entlasten einbinden (z.B. Proxy mit Backend) 
C) Varnish-Cash -> System durch vorgeschaltet Systeme entlassen 

```

## IO gebundene Last erkennen und handeln 

```
# Habe ich einen io-gebunden oder cpu-gebundene Last

# IO-gebundene Last 
# Was heisst das ?
Die CPU wartet auf die Festplatte, die Festplatte knirscht
und kann nicht mehr abarbeiten, sie ist durch die Arbeit
die Arbeit voll ausgelastet.

# Wie finde ich das heraus ?
top
1) In der Übersicht: CPus: us und u.U. sy wert Hoch 
2) load average hoch:
Spalte 1: Wieviele Prozesse warteten im Durchrschnitt auf Ausführung durch die CPU in der letzten Minute
Spalte 2: Das gleiche wie 1 nur in den letzten 5 Minuten 
Spalte 3: Das gleiche wie 1 nur in den letzten 15 Minuten
-> 3) In CPU-Zeile: wa-wert ist HOCH  oder niedrig. <-

# Was tun ? 
A) Schnellere Platte kaufen (hdd -> ssd - platte) 
B) Weitere Systeme zu Entlasten einbinden (z.B. Proxy mit Backend) 
C) Varnish-Cash -> System durch vorgeschaltet Systeme entlassen 

```

## Werte einstellungen

```
# Welche Kind am Starten werden restarten/gestartet wird
# Default 3 
StartServers  

# Hard limit für Thread pro Kind-Prozess 
# Wieviele ThreadPerChild (Threads pro Kind kann ich maximal konfigurieren)
# Standardmäßig: 64 
ThreadLimits 

# Wieviel Threads per Child (max. ThreadLimits) werden beim Bereitstellen
# eines neune Child erstellt 
# Standard ist 25 
# 25 ist good to go. 
# Wenn höher unbedingt 
ThreadsPerChild 

# Maximale Zahl an Kind-Prozessen 
# z.B. 4 Prozesse (die Threads sind damit nicht gemeint)
ServerLimit 

# Maximale Anzahl aller Threads  über alle jobs  
MaxRequestWorkers = 200 # vorher MaxClient vor 2.3 aktuell geht noch beides 

# MinSpareThreads 
# unbeschäftigte Threads, werden hochgefahren, wenn nicht genügen unbeschäftigte
# Threads vorhanden sind. 

# MaxSpareThreads 

```

