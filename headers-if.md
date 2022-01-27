# Rewrite Headers on If 

## Example 

```
# Set response header if url contains 'test'
<If "%{REQUEST_URI} =~ /test/">
   Header set MegaHeader 'Cool stuff'
</If>

```


## Refs:

  * [Expression - Important reference](https://httpd.apache.org/docs/2.4/expr.html)

