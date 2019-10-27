sgws_config
===========

This role and modules are intended to configure a NetApp StorageGRID. The following tasks can be performed:

- Authorize to get a token
- Install signed SSL certificates
- Setup an Identity provider
- Create a local or federated group


Requirements
------------

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) needs to be installed.

Role Variables
--------------

Settable variables for the role are in `roles/sgws_config/vars/main.yml`. Passwords and credentials are incorporated using [ansible-vault](https://docs.ansible.com/ansible/latest/cli/ansible-vault.html). Other variables are under `roles/sgws_config/vars/` for their respective tasks.

Installing signed API management SSL certificates requires three files `mgmt_cert.pem`, `mgmt_cert.key` and `chain.pem` to be in `roles/sgws_config/files`. Storage API SSL certificate files are `stor_cert.pem`, `stor_cert.key` and `chain.pem`.

Dependencies
------------

There are no dependencies.

Example Playbook
----------------

```bash
# ansible-playbook --vault-password-file ~/.passwd sgws_config.yml

PLAY [sgws] ***************************************************************************

TASK [sgws_config : Get grid authorization token] *************************************
ok: [localhost]

TASK [sgws_config : Load account variables] *******************************************
ok: [localhost]

TASK [sgws_config : Gather accounts list] *********************************************
ok: [localhost]

TASK [sgws_config : Looking if account "Widgets Unlimited" exists] ********************
skipping: [localhost]

TASK [sgws_config : Crate new storage tenant account "Widgets Unlimited"] *************
ok: [localhost]

TASK [sgws_config : Get org authorization token] **************************************
ok: [localhost]

TASK [sgws_config : Load tenant's identity variables] *********************************
ok: [localhost]

TASK [sgws_config : Set or update identity source for tenant] *************************
ok: [localhost]

TASK [sgws_config : Load tenant's group variables] ************************************
ok: [localhost]

TASK [sgws_config : Check if tenant's group "Developers" exists] **********************
ok: [localhost]

TASK [sgws_config : Crate new tenant's "Developers" group] ****************************
ok: [localhost]

TASK [sgws_config : Generate S3 access key for tenant] ********************************
ok: [localhost]

TASK [sgws_config : Generate S3 keys] *************************************************
ok: [localhost]

TASK [sgws_config : Save generated S3 keys] *******************************************
changed: [localhost]

PLAY RECAP ****************************************************************************
localhost                  : ok=13   changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

License
-------

GPL

Author Information
------------------

- Adly Taibi

