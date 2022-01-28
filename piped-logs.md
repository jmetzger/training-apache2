# Using Piped Logs 

## Example 

```
CustomLog "|/bin/grep -v '^200' | cat >> /var/log/apache2/pi-mirror.com/access.log" combined

# Not sure, if this works too: 
CustomLog "|/bin/grep -v '^200' >> /var/log/apache2/pi-mirror.com/access.log" remove

```


## Refs:

  * https://workshop.avatarnewyork.com/post/filtering-apache-piped-logs-to-centralize-logging-of-errors-and-warnings/
  * https://httpd.apache.org/docs/2.4/logs.html#piped
