# Script for finding all modules configured to be loaded (Centos / Redhat)

```
for i in /etc/httpd/conf.modules.d/*; do cat $i | grep LoadModule | sed 's/^ *//' | cut -d' ' -f2 ; done

# or simply 
httpd -M | cut -d' ' -f2

```

```
# Finds all IfModule entries 
for i in $(httpd -M | cut -d' ' -f2); do  grep -r $i /etc/httpd | grep -v LoadModule  ; done


```

