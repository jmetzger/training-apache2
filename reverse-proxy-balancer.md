# Reverse Proxy Balancer 

## Example 

```

<Proxy "balancer://mycluster">
   BalancerMember "http://10.135.0.9"
   BalancerMember "http://10.135.0.12"
</Proxy>

# important to set / twice in line 
# If you set it as last char in first column, and also has to be at the end of URL 
# DOES NOT WORK for sub pages: ProxyPass "/" "balancer://mysqlcluster"
# USE THIS -> 
ProxyPass        "/" "balancer://mycluster/"
ProxyPassReverse "/" "balancer://mycluster/"

```

## Sticky Session Id for php (sticky session explained)

  * http://www.markround.com/archives/33-Apache-mod_proxy-balancing-with-PHP-sticky-sessions.html

## References 

  * https://httpd.apache.org/docs/2.4/mod/mod_proxy_balancer.html 
