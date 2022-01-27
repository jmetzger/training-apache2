# mod_rewrite 


## Rewriting aktivieren

```
RewriteEngine on 
```

## Rewrite - bessere Alternative ? 

```
# Rewriting sollte das last resort sein,
# Wenn man eine Alternative hat, sollte man dieser verwendet,
# weil rewriting weniger performant 
# z.B. bei Alias / Redirect 

```

## Mod_rewrite schwierig zu debuggen.

```
Alternativ kann sein, alle Anfragen immer an das gleiche 
Script zu leitern und dort zu verarbeiten, z.B. mit redirect

Warum ?
Im Script kann man leichter debuggen. 

```

## Logging einschalten / abschalten 

```
RewriteLog "/var/www/mod_rewrite.log"
RewriteLogLevel 2
```

## Ref: 

  * https://httpd.apache.org/docs/trunk/rewrite/intro.html
