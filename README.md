[![Build Status](https://travis-ci.org/CSCfi/ansible-role-shibboleth-proxy.svg?branch=master)](https://travis-ci.org/CSCfi/ansible-role-shibboleth-proxy)

Ansible-Role: Shibboleth Proxy
=========

An role which installs Shibboleth Proxy on RedHat/Debian servers. 

Requirements
------------
* ansible 2.5 <

Role Variables
--------------

See defaults/main.yml for the variables you can overwrite via role call via parameter
You can also pass configurables array for role. This array contains extra configurable items for shibboleth proxy such as

For extra functionality
* flows
* disco

See example playbook for calling role with configurable array and overwritable attributes

Dependencies
------------

* [CSCfi.jetty](https://github.com/CSCfi/ansible-role-jetty) 
* [CSCfi.mariadb](https://github.com/CSCfi/ansible-role-mariadb) (Optional, configurable nameid uses database storage )
* [CSCfi.apache](https://github.com/CSCfi/ansible-role-apache)
* [CSCfi.shibboleth-idp](https://github.com/CSCfi/ansible-role-shibboleth-idp)
* [CSCfi.shibboleth-sp](https://github.com/CSCfi/ansible-role-shibboleth-sp)

Example Playbook
----------------

    - hosts: all
      vars:
        shibbolethidp_configurables: ['ldap','shibsp','oidc','disco','certs']
       	shibbolethidp_jetty_secure_port: 8443
        shibbolethidp_mpassidrelease: 0.9.4

        shibbolethsp_configurables: ['certs']

        ansible_fqdn: my.proxy.localhost

        apache_configurables: ['certs']
	
      roles:
      	- { role: CSCfi.shibboleth-proxy, configurables: ['flows','disco'] }
