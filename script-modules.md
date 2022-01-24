# Script for finding all modules configured to be loaded (Centos / Redhat)

```
for i in /etc/httpd/conf.modules.d/*; do cat $i | grep LoadModule | sed 's/^ *//' | cut -d' ' -f2 ; done

```
