# MIT-Kerberos + LDAP

## Additinal clients

1. configure or disable SELinux
2. configure or disable firewall?
3. update /etc/hosts
4. dnf install krb5-workstation
5. dnf install sssd-tools
6. set /etc/sssd/sssd.conf
7. set /etc/krb5.conf
8. authselect sssd
9. echo "session optional pam_oddjob_mkhomedir.so skel=/etc/skel/ umask=0022" >> /etc/pam.d/system-auth
10. systemctl enable --now oddjobd
11. copy ldap public cert to /etc/openldap/certs/
12. Also cert refrenced in sssd.conf
    * /etc/pki/tls/cacert.crt

13. from kadmin server

`kadmin`

`kadmin: addprinc random host/linux.heer.net`

`kadmin: ktadd -k /tmp/krb5.keytab host/linux3.heer.net`

14. copy /tmp/krb5.keytab to client server into /etc

### Test with LDAP first
1. Temporarly adjust sssd.conf
    `auth_provider = krb5`

    to

    `auth_provider = ldap`

#### SSH
- Server Daemon
/etc/ssh/sshd_config

`GSSAPIAuthentication yes`

`GSSAPICleanupCredentials yes`

`systemctl restart sshd`

- Client
/etc/ssh/ssh_config

`GSSAPIAuthentication yes`

`GSSAPIDelegateCredentials yes`

