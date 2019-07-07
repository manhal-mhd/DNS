mnhl_dns
=========

this role is meant to configure master and slaves DNS Authertative servers , with diffrent view for the internal "trusted" network where recursion is enabled , and view for external "untrusted" network where recursion is disabled.
also it configer a TSIG for zone transfer from master ad slaves for each network  

Requirements
------------

this role uses TSIG keys for zone transfer between master and slave/s

Role Variables
--------------

* [internal_key:]   key for internal network zone transfer 
* [ external_key:] key for external network zone transfer
* [ master:] ip address of master DNS server
* [slaves:] list of IPs of slaves servers 
* [listen_ipv4:] network interfaces ipv4 that DNS is allowed to listen on 
* [listen_ipv6:] network interfaces ipv6 that DNS is allowed to listen on 
* [dns_acl_internal:] ACL for trusted network 
* [dns_acl_external:] ACL for untrusted network
* [forwarders:] list of name resolvers IP addressess 
  

Dependencies
------------

to generate TSIG keys : 
dnssec-keygen -a HMAC-SHA512 -b 512 -n HOST -r /dev/urandom internal
dnssec-keygen -a HMAC-SHA512 -b 512 -n HOST -r /dev/urandom external 

; please use the key in .private generated file  

Example Playbook
----------------

---
- name: configuer DNSs 
  hosts: all
  gather_facts: false
  roles: 
     - mnhl_dns

License
-------

BSD

Author Information
------------------
Name: Manhal Mohammed Mokhtar 
Email: manhal.mhd@gmail.com
 
