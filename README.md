sgws_config
===========

This role and modules are intended to configure a NetApp StorageGRID. The following tasks can be performed:

- Authorize to get a grid token
- Install signed SSL certificates for API management
- Install signed SSL certificates for Storage management
- Setup an Identity provider
- Create a local or federated group for admin
- Authorize to get a tenant token
- Setup an Identity provider for tenant
- Create a local or federated group for tenant
- Generate S3 keys for tenant
- Create bucket for tenant

Requirements
------------

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) needs to be installed.

Role Variables
--------------

Settable variables for the role are in `roles/sgws_config/vars/main.yml`. Passwords and credentials are incorporated using [ansible-vault](https://docs.ansible.com/ansible/latest/cli/ansible-vault.html). Other variables are under `roles/sgws_config/vars/` for their respective tasks.

Installing signed API management SSL certificates requires three files `mgmt_cert.pem`, `mgmt_cert.key` and `chain.pem` to be in `roles/sgws_config/files`. Storage API SSL certificate files are `stor_cert.pem`, `stor_cert.key` and `chain.pem`.

Turn on or off plays in `roles/adlytaibi.sgws_config/tasks/main.yml` by commenting or uncommenting the respective lines.

Since there is prerequisite work to perform prior to using some plays. SSL certificate and identity provider play are commented out by default.

Dependencies
------------

There are no dependencies.

Example Playbook
----------------

```bash
# ansible-playbook --vault-password-file ~/.passwd .ansible/roles/adlytaibi.sgws_config/sgws_config.yml

PLAY [sgws] **********************************************************************************************************************

TASK [adlytaibi.sgws_config : Get grid authorization token] **********************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Load admin group variables] ************************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Check if group "Developers" exists] ****************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Crate new administrators "Developers" group] *******************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Load account variables] ****************************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Gather accounts list] ******************************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Looking if account "Widgets Unlimited" exists] *****************************************************
skipping: [localhost]

TASK [adlytaibi.sgws_config : Crate new storage tenant account "Widgets Unlimited"] **********************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Get org authorization token] ***********************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Load tenant's group variables] *********************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Check if tenant's group "Developers" exists] *******************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Crate new tenant's "Developers" group] *************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Load S3 access key for tenant variables] ***********************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Generate S3 keys] **********************************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Save generated S3 keys] ****************************************************************************
changed: [localhost]

TASK [adlytaibi.sgws_config : Load bucket for tenant variables] ******************************************************************
ok: [localhost]

TASK [adlytaibi.sgws_config : Create a bucket] ***********************************************************************************
ok: [localhost]

PLAY RECAP ***********************************************************************************************************************
localhost                  : ok=16   changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

```

License
-------

GPL

Author Information
------------------

- Adly Taibi

