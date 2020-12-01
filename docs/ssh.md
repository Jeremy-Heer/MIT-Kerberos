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