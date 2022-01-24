# lsof (List open files) 

```
# Zeigt alle ports an auf die gelauscht wird (ipv4) 
# Ist httpd in der Liste 
lsof -i 
# alternative
netstat -tupel

# Wie heisst dort Port als Nummer ? 
cat /etc/services | grep "^httpd " 

```
