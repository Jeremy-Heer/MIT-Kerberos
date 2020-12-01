# kadmin / kadmin.local
- kadmin.local can only be ran on the KDC server unless the KDC is using an LDAP database

## Used to administer the kerbeos database
- Manage principles
- Manage policies
- Manage keytab files

## Initial setup
1. Add an admin principle from the KDC for furture administration.
1. Add principles and keytabs for hosts hosting kerberos protected services
1. Add principles for users


## Adding Principles for administration

Assuming our admin user will be "krbadmin":

1. `kadmin.local`
1. `kadmin.local: addprinc krbadmin/admin`
1. Type and confirm the password for krbadmin
1. `quit`

You can now validate the admin user by launching kadmin with -p
1. `kadmin -p krbadmin/root`
1. Type the password when prompted

## Adding Principles and Keytabs for hosts hosting kerberos protected services

Assuming our hostname of our kerberos service is server1.krbtest.net

To add the principale:

1. Launch kadmin or kadmin.local
1. `kadmin: addprinc -randkey host/server1.krbtest.net`

If your running kadmin from the KDC, ou will want to specify a keytab file. Otherwise kadmin will add it to the default keytab on the server (/etc/krb5.keytab)

1. launch kadmin or kadmin.local
1. If running kadmin locally on the KDC:
1. `kadmin: ktadd -k /tmp/krb5.keytab host/server1.krbtest.net`
1. Copy the /tmp/krb5.keytab file to your destination servers /etc folder then remove from the KDC /tmp folder
1. Or if running kadmin on the remote server hosting the kerberos protected service:
1. `kadmin: ktadd host/server1.krbtest.net`
1. This will create it directly in the default /etc folder