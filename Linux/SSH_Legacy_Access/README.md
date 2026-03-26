# SSH access to legacy network devices

## Problem

Modern OpenSSH clients disable older cryptographic algorithms by default (e.g. `ssh-rsa`, `diffie-hellman-group1-sha1`).

As a result, connections to many legacy network devices (Cisco, Juniper, etc.) fail with errors like:

* "no matching key exchange method"
* "no matching host key type"

## Impact

This issue affects a large number of older devices still running in production environments, especially in service provider networks.

## Solution

This configuration enables legacy SSH algorithms to restore connectivity to such devices.

```bash
Host *
User your-user
HostKeyAlgorithms ssh-rsa,ssh-dss
KexAlgorithms diffie-hellman-group1-sha1
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc
```

## Use Case

Used in real-world environments to access and manage legacy routers and switches where upgrading is not immediately possible.

## ⚠️ Security Notice

These algorithms are considered insecure and should only be used when absolutely necessary (e.g. legacy systems).
They should not be enabled globally in modern secure environments.

## Goal

Provide a quick and practical workaround to maintain operational access to legacy infrastructure.
