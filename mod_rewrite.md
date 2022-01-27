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

## Logging einschalten 

```
# highest loglevel -
LogLevel rewrite:trace8
```
## Beispiel 1: alte Domain auf Neue Domain umleiten

```
# Redirect all pages from olddomain.com
# to newdomain.com
RewriteEngine on
RewriteCond %{HTTP_HOST} ^jobs.jochen.t3isp.de$ [OR]
RewriteCond %{HTTP_HOST} ^www.jobs.jochen.t3isp.de$
# $1 bezieht sich auf die 1. Klammer
# http://www.jobs.jochen.t3isp.de/test.html 
# ^(.*)$ = /test.html
RewriteRule ^(.*)$ http://casino.jobs.jochen.de/$1 [R=301,L]

```
## Beispiel 2: Unterordner erzwingen 

```
RewriteEngine On
RewriteRule ^$ /folder/ [R=301,L]

```

## Beispiel 3: Unterseite erzwingen

```
RewriteEngine On
RewriteRule ^$ /unterseite.html [R=301,L]
```

## Beispiel 4: Bestimmte Dateien nicht erlauben

```
#Do not allow these file types to be called
RewriteEngine on
RewriteRule .*\.(jpg|jpeg|gif|png|bmp|exe|swf)$ - [F,NC]


```

## Beispiel 5: Rewrite only, if it does not exist 

```
RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-l

RewriteRule .* index.php [L]
```


## Ref: 

  * https://httpd.apache.org/docs/trunk/rewrite/intro.html
