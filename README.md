# MIT-Kerberos + LDAP

## Environment

### Servers
| Server Name    | Description | OS | IP |
| -------------- | ----------- | -- | -- |
| NETWORK1       | DNS  | Windows Server 2019 | 10.1.1.1 |
| KDCLDAP1       | KDC / LDAP  | Oracle Linux | 10.1.1.2 |
| LINUNX1        | Linux Client | Oracle Linux | 10.1.1.10 |
| SOLARIS1       | Solaris Client | Solaris 11 x86 | 10.1.1.11 |

* DNS Name: `krbtest.com`
* REALM: `KRBTEST.COM`

### LDAP Directory Structure

* `dc=krbtest,dc=com`

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

### Other links

[SSH](docs/ssh.md)


