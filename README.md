[![Build Status](https://travis-ci.org/CSCfi/ansible-role-shibboleth-idp-proxy.svg?branch=master)](https://travis-ci.org/CSCfi/ansible-role-shibboleth-idp-proxy)

Ansible-Role: Shibboleth IdP Proxy
=========

A role which installs Shibboleth IdP Proxy on RedHat/Debian servers. 

Can be used to proxy authentication requests from SAML2 or OpenID Connect services to SAML2 Identity Providers. Support for OpenID Connect providers is not in the current release. Provides a discovery page where user can select preferred authentication.

Built from these components:
* Shibboleth IdP 3
* Shibboleth SP 3
* https://github.com/mpassid/shibboleth-idp-authn-shibsp
* https://github.com/mpassid/shibboleth-idp-authn-discovery
* https://github.com/CSCfi/shibboleth-idp-oidc-extension


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
        shibbolethidp_configurables: ['ldap','oidc','certs']
        shibbolethidp_jetty_secure_port: 8443
        shibbolethidp_mpassidrelease: 0.9.4

        shibbolethsp_configurables: ['certs']

        ansible_fqdn: my.proxy.localhost

        apache_configurables: ['certs']
	
      roles:
      	- { role: CSCfi.shibboleth-proxy, configurables: ['flows','disco'] }
