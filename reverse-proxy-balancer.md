# Reverse Proxy Balancer 

## Example 

```

<Proxy "balancer://mycluster">
   BalancerMember "http://10.135.0.9"
   BalancerMember "http://10.135.0.12"
</Proxy>

ProxyPass        "/" "balancer://mycluster"
ProxyPassReverse "/" "balancer://mycluster

```
