# Overview

This ansible role is used to configure a client to establish a tunnel with
a gateway server.  For inbound connection autossh is used to establish remote
port forward connections over ssh and to keep those sessions alive.  For outbound
proxying through the gateway, sshuttle is used to forward outbound packets over
ssh.

Currently, the role is hardcoded to remote port forward ports required for running
a mail server (ie. 25, 443, 587, 993, 8443) and port 80 meant for certificate management
tasks.  The outbound sshuttle proxy is configured to send all traffic through
the gateway except for local addresses (192.168.0.0/16, 10.0.0.0/8, and 172.16.0.0/12).

# Dependencies
A gateway server with a public IP address that has sshd configured to allow
gateway ports.  The role obtains the address of the gateway by looking for
an ansible host named 'gateway'.  You can configure this by adding the gateway
host to your ansible inventory file.  Or, if you are dynamically creating the
gateway as part of a playbook the 'gateway' host can be added through the
add_host ansible module.



# Variables
```yaml
- vars:
  autossh: [true|false] # install and configure autossh for inbout port forwarding
  sshuttle: [true|false] # install and configure sshuttle outbound proxy
```
