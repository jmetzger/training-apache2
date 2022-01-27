# Security headers apache 

## Important headers 

```
Strict-Transport-Security	max-age=31536000
Content-Security-Policy 
X-Frame-Options
X-Content-Type-Options
Referrer-Policy	
Permissions-Policy
```
## Set in apache 

```
# /etc/httpd/conf.d/z_security.conf 
Header always set Content-Security-Policy "default-src 'self'; font-src *;img-src * data:; script-src *; style-src *;"
Header set X-XSS-Protection "1; mode=block"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-Content-Type-Options "nosniff"
Header always set Referrer-Policy "strict-origin"
Header always set Permissions-Policy "geolocation=(),midi=(),sync-xhr=(),microphone=(),camera=(),magnetometer=(),gyroscope=(),fullscreen=(self),payment=()"
```

## Reference 

  * https://webdock.io/en/docs/how-guides/security-guides/how-to-configure-security-headers-in-nginx-and-apache


