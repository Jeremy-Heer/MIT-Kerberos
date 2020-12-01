## Basic OS setup
1. Will be using [Oracle Virtual Box](https://www.virtualbox.org/)
1. Will be using [CentOS 8.2](https://www.centos.org/)
1. Configure and start a new VM using the above .iso
    * Choose a network option that will have access to the Internet
1. Right Ctrl will release the mouse during the OS install
1. These options don't matter much but I normally
    * Server with GUI
    * disable kdump
    * default partitioning
1. Make sure network is configured
    * hostname: "server1.krbtest.net"
    * Toggle to "ON"
1. Begin Installation
1. Create a local user and set the root password
    * localuser: Password1
    * root: Password1
1. Eject the DVD and reboot
1. Optional: Add guest additions
    * as root: `dnf update`
    * As root: `dnf install epel-release`
    * As root: `dnf install gcc make perl kernel-devel kernel-headers bzip2 dkms`
    * reboot
    * Devices / Insert Guest Additions CD image
    * More info [HERE](https://www.tecmint.com/install-virtualbox-guest-additions-on-centos-8/)
1. Adjust /etc/hosts
    * [actual IP] server1.krb5test.net
1. Disable or adjust SELinux
    * As root: vi /etc/selinux/config
    * `SELINUX=disabled`
    * reboot
1. Disable or adjust firewall
    * As root: `systemctl stop firewalld`
    * As root: `systemctl disable firewalld`
    * or
    * As root: `systemctl start firewalld.service`
    * As root: `firewall-cmd --add-service=kerberos --permanent`
    * As root: `firewall-cmd --add-service=kadmin --permanent`
    * As root: `systemctl restart firewalld.service`
    * As root: `systemctl enable firewalld.service`