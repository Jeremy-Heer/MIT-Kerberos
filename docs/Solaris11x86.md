## General Commands
* To shutdown `shutdown -y -g0 -i5`
* List current hostname `svccfg -s system/identity:node listprop config`
* Update hostname
    * `svccfg -s system/identity:node setprop config/nodename="yournewhostname"`
    * `svcadm refresh system/identity:node`
    * `svcadm restart system/identity:node`
* Update DNS client
    * just update /etc/hosts. There is a better way but this is fine for testing.

## Tasks to use LDAP for system authentication

## To list properties of name-service 
* svcprop name-service/switch:default

* View LDAP client state
    * `svcs ldap/client`

* Assuming you have a working LDAP server with [RFC207Bis Schema](https://ldapwiki.com/wiki/SchemaRFC2307Bis)
* And a sample LDAP structrue like [THIS](samples/BasicLDAP.ldif)

1. Backup current nsswitch.conf
    1. cp /etc/nsswitch.conf /etc/nsswitch.conf.back
1. Apply sample LDAP nsswitch
    1. cp /etc/nsswitch.ldap /etc/nsswitch.conf
1. Make sure only desired options are set to LDAP. Probably want to keep hosts and ipnodes at `files dns`.
1. Applied
    1. nscfg import -f name-service/switch
1. Update default domain
    1. echo "example.com" > /etc/defaultdomain
1. Update ldapclient
    1. `ldapclient init -v -a proxyDN=cn=proxyagent,ou=profile,dc=example,dc=com -a proxyPassword=secret -a domainName=example.com -a profileName=testprofile linux1.example.com:1389`
1. Validate
    1. `ldaplist` (Should display LDAP OUs)
    2. `getent passwd` (Should list LDAP users)

## Update Pam stack
1. /etc/pam.d/login
    * change this `auth required           pam_unix_auth.so.1`
    * to this `auth binding           pam_unix_auth.so.1  server_policy`
    * add this `auth required		pam_ldap.so.1`
1. /etc/pam.d/other
    * change this `auth required           pam_unix_auth.so.1`
    * to this `auth binding           pam_unix_auth.so.1 server_policy`
    * add this `auth required		pam_ldap.so.1`
1. Refresh name-service
    * `svccfg -s system/name-service/switch`
    * `refresh`
    * `quit`
1. Validate
    1. `su sholems`

* https://www.youtube.com/watch?v=9kGK26A400Q&t=2098s