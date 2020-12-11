# General cert related commands

- Obtaining the public cert from a running ldap server

1. `openssl s_client localhost:1636|openssl x509 -out /tmp/ldap2.der -outform der`
1. `openssl x509 -out /tmp/ldap2.crt -outform pem -text -in /tmp/ldap2.der -inform der`

### Refrence the ldap2.crt in sssd.conf and store in /etc/openldap/certs