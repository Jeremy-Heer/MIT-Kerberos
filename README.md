# MIT-Kerberos

## Additinal clients

configure or disable SELinux
configure or disable firewall?

update /etc/hosts
dnf install krb5-workstation
dnf install sssd-tools

set /etc/sssd/sssd.conf
set /etc/krb5.conf

authselect sssd

systemctl enable --now oddjobd
echo "session optional pam_oddjob_mkhomedir.so skel=/etc/skel/ umask=0022" >> /etc/pam.d/system-auth
systemctl enable --now oddjobd

copy ldap public cert to /etc/openldap/certs/
Also cert refrenced in sssd.conf
/etc/pki/tls/cacert.crt

from kadmin server:
kadmin
kadmin: addprinc random host/linux.heer.net
kadmin: ktadd -k /tmp/krb5.keytab host/linux3.heer.net

copy /tmp/krb5.keytab to clien server into /etc

Temporarly adjust sssd.conf
from
auth_provider = krb5
to
auth_provider = ldap

verify LDAP first

ssh deamon and client
/etc/ssh/sshd_config
GSSAPIAuthentication yes
GSSAPICleanupCredentials yes

/etc/ssh/ssh_config
GSSAPIAuthentication yes
GSSAPIDelegateCredentials yes
systemctl restart sshd
