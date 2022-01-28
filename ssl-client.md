# Clientbasierte SSL Authentifizierung 

## Walkthrough (RHEL/Rocky) 

```
mkdir -p /usr/local/src/SSL
cd /usr/local/src/SSL

# Schritt 1: ROOT-CA erstellen (firmenweit) 
openssl genrsa -out ssl.netways.de_rootca.key 4096

# Schritt 2: ROOT-CA Zertifikat erstellen  
openssl req -x509 -new -nodes -key ssl.netways.de_rootca.key -sha256 -days 3650 -out ssl.netways.de_rootca.pem

# Schritt 3: Key für Client erstellen 
openssl genrsa -out ssl.netways.de_client1.key 4096

# Schritt 4: CSR (Certificate Signing Request erstellen) 
openssl req -new -key ssl.netways.de_client1.key -out ssl.netways.de_client1.csr

# Schritt 5: Struktur für OpenSSL anlegen (default Verzeichnise, einkompiliert in openssl
mkdir -p demoCA/newcerts && mkdir demoCA/certs && mkdir demoCA/crl && echo 00 > demoCA/serial && touch demoCA/index.txt

# Schritt 5a:
# vi demoCA/openssl.cfg
#
# SSLeay example configuration file.
# This is mostly being used for generation of certificate requests.
#

RANDFILE            = ./.rnd

####################################################################
[ req ]
default_bits        = 2048
default_keyfile     = keySS.pem
distinguished_name  = req_distinguished_name
encrypt_rsa_key     = yes
default_md          = sha1

[ req_distinguished_name ]
countryName         = Country Name (2 letter code)

organizationName    = Organization Name (eg, company)

commonName          = Common Name (eg, YOUR name)

####################################################################
[ ca ]
default_ca         = CA_default        # The default ca section

####################################################################
[ CA_default ]

dir                = ./demoCA              # Where everything is kept
certs              = $dir/certs            # Where the issued certs are kept
crl_dir            = $dir/crl              # Where the issued crl are kept
database           = $dir/index.txt        # database index file.
#unique_subject    = no                    # Set to 'no' to allow creation of
                                           # several certificates with same subject.
new_certs_dir      = $dir/newcerts         # default place for new certs.

certificate        = $dir/cacert.pem       # The CA certificate
serial             = $dir/serial           # The current serial number
crl                = $dir/crl.pem          # The current CRL
private_key        = $dir/private/cakey.pem# The private key
RANDFILE           = $dir/private/.rand    # private random number file

name_opt           = ca_default            # Subject Name options
cert_opt           = ca_default            # Certificate field options

default_days       = 365                   # how long to certify for
default_crl_days   = 30                    # how long before next CRL
default_md         = md5                   # which md to use.
preserve           = no                    # keep passed DN ordering

policy             = policy_anything

[ policy_anything ]
countryName            = optional
stateOrProvinceName    = optional
localityName           = optional
organizationName       = optional
organizationalUnitName = optional
commonName             = supplied
emailAddress           = optional



# Schritt 6: csr unterschreiben lassen 
openssl ca -in ssl.netways.de_client1.csr -cert ssl.netways.de_rootca.pem -keyfile ssl.netways.de_rootca.key -out ssl.netways.de_client1.crt -days 3650 -config demoCA/openssl.cfg

# Schritt 7: anderes Format erstellen für Import 
openssl pkcs12 -export -in ssl.netways.de_client1.crt -inkey ssl.netways.de_client1.key -out NETWAYS_Client_gmimietz.p12



```



## Where to store the ca-cert (Different on RHEL and Debian) 

  * https://stackoverflow.com/questions/37043442/how-to-add-certificate-authority-file-in-centos-7

## Refs:

  * https://www.netways.de/blog/series/ssl-leicht-gemacht/
