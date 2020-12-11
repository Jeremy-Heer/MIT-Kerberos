## Basic KDC setup
1. Assuming you have a [server ready](CentOS8-2.md)
1. As root: `dnf install krb5-server krb5-workstation`
1. Edit the /etc/krb5.conf
    * Uncoment all lines and sections with example.com
    * replace example.com with your domain / REALM
    * update the kdc and admin to your server name
1. Edit the /var/kerberos/krb5kdc/kadm5.acl
    * update the realm data
1. Edit the /var/kerberos/krb5kdc/kdc.conf
    * update the realm name in the [realms] section

## Master KDC
1. Complte the Basic KDC setup above
1. Create the KDC database
    * `kdb5_util create -s -r KRBTEST.NET`
    * Enter a database master key when prompted
1. Enable and start the kerberos deamons
    * `systemctl enable krb5kdc`
    * `systemctl enable kadmin`
    * `systemctl start krb5kdc`
    * `systemctl start kadmin`

## Replica KDCs
1. Complte the Basic KDC setup above
1. 