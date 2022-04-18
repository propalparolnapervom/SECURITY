# SSH

## Overall

`Ssh-keygen` is a tool for creating new authentication key pairs for SSH. Such key pairs are used for automating logins, single sign-on, and for authenticating hosts.

`OpenSSH` is an open source implementation of the `SSH` protocol.

> **NOTE**: `OpenSSH` does not support `X.509` certificates. `Tectia SSH` (commercial implementation of SSH) does support them.
> `OpenSSH` has its own proprietary certificate format, which can be used for signing host certificates or user certificates.

`SSH` provides an authentication mechanism based on cryptographic keys, called `public key authentication`. 

One or more `public keys` may be configured as `authorized keys`.  

The `private key` corresponding to an `authorized key` serves as authentication to the server. 


The keys used for user authentication are called `user keys`. SSH also uses `host keys` for authenticating hosts. Together these are called `SSH keys`.

The `authorized_keys` file in SSH specifies the `SSH keys` that can be used for logging into the user account for which the file is configured.

With OpenSSH, the `authorized keys` are by default configured in `.ssh/authorized_keys` in the user's home directory. The file lists keys that are authorized for authenticating as that user, one per line.



## Generate

Generate public/private rsa key pair

> **NOTE**: By default, generated key is placed as `~/.ssh/id_rsa`
```
# Specify RSA algorythm
ssh-keygen -t rsa

# Specify the length (bit size) of the key 
ssh-keygen -b 2048 -t rsa

# Specify the output file location/name
ssh-keygen -t rsa -f /tmp/to_del/cert-selfsigned/private_ssh_key
```









































