# Gegenüberstellung mpm-Module 

## Begriff

```
# Multi Processing Module 
```

## Welche gibt es ? 

  * mpm_prefork 
  * mpm_worker
  * mpm_event 

## mpm_prefork 

  * Pro Abfrage, ein Prozess 
  * Verwendung nur im "Notfall", d.h. wenn nichts anderes geht 
  * z.B. bei php (als Modul) nur prefork funktioniert 

## mpm_worker 

  * Beim mpm-worker modul arbeiten die Threads die Anfragen ab. 

```
# parent- process unter root

# startet Kind-Prozesse 
# Threads sind leichtgewichtiger 

# Ich kann mehr aus mehr aus meinem Server rausholen/rausquetschen
# bei gleicher CPU und Arbeitsspeicher 

# Weil in einem Prozess bei gleichem Arbeitsspeicher mehr Threads reinpassen
# als wenn ich das nur wie bei mpm_prefork über Prozesse darstellen 

```

## mpm_event 

```
# ein Prozess start seine Worker-Threads + 1 Listening Thread 

# Listening Thread lauscht nach draussen, nimmt Anfrage und gibt sie 
# weiter an einen freien Worker-Thread 

```
