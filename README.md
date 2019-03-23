SUSEConnect
===========

Use this role to connect a SUSE Linux system to the SUSE Customer Center or a local SMT server. You can also specify which add-on products are to be registered.

Requirements
------------

You'll need the registration key that came with your SUSE subscription. For some products you'll need extra registration keys. You'll also need to know the internal product name of the product you're trying to register. I'll try to provide a full list in a README file.

Role Variables
--------------

You can set the following variables:

    suseconnect_products:             # list, products that should be activated on the target system
      - product:                      # string. internal product name, see PRODUCTS.md for a list
        version:                      # string, product version that should be activated, defaults to the major version of the base os
        arch:                         # string, architecture of the product to be actived, defaults to the arch of the OS (ansible_machine)
        key:                          # string, if the product needs an additional registration key
    suseconnect_reregister:           # bool, register all products regardless of current status
    suseconnect_remove_subscriptions: # bool, remove currently registered products, absent in suseconnect_products

This variable is used, but should not be set by the user:

    suseconnect_binary:     # string, path of the SUSEConnect binary

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - role: b1-systems.suseconnect
       vars:
         suseconnect_os_key: '12345ABCDE'
         suseconnect_products:
           - product: 'sle-sdk'
             version: '12.2'
             arch: 'x86_64'
           - product: 'SUSE-Manager-Server'
             version: '4.0'
             key: '123SUMAKEY34'
           - product: sle-module-web-scripting
           - product: sle-module-python2
```

License
-------

GPLv3

Author Information
------------------

Sebastian Meyer (meyer@b1-systems.de)
B1 Systems GmbH
