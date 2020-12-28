# Plugable Authentication Modules

## File Structure
```
/lib
    | libpam.so.0
    | security
        | pam_unix.so
        | pam_deny.so
/etc
    | pam.conf
    | pam.d
        | login
        | ssh
        | other
    | security
        | access.conf
        | pam_mount.conf
/usr
    | include
        | security
            | pam_modules.h
```

## pam.conf Syntax

`<service>    <type>    <control>    <module-path>    <module-arguments>`

#### Example
```
login auth   required   pam_unix.so nullok_secure
login auth   optional   pam_mount.so use_first_pass debug
login auth   optional   pam_ssh.so use_first_pass debug
```

## Service (Column 1)

* login

* su

* ssh

## Type (Column 2)

### account

* Non-authentication based account management
* typically used to restrict/permit access to a service based on the time of day, currently available system resources (max number of users) or perhaps the location of user

### auth

* establishes that the user is who they claim to be

### password

* Required for updating the authentication token associated with the user.

### session

* associated with doing things that need done before/after they can be given service. Such as logging, opening/closing of some data exchange with user, mounting directories, etc.

## Control (Column 4)

* required

* requisite

* sufficient

* optional

* include

* substack
