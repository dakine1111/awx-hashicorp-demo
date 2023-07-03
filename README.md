# Login to vault and run playbook
```bash
export VAULT_ADDR=https://<YOUR_VAULT_SERVER>
vault login -method ldap -tls-skip-verify username=<AD Username>
ansible-playbook play.yml
```

# AAP configuration
## Create new Credential Type
Name: Hashi vault
Input configuration:
```yaml
fields:
  - id: vault_server
    type: string
    label: URL for Vault Server
  - id: vault_role_id
    type: string
    label: Role ID
  - id: vault_secret_id
    type: string
    label: Secret ID
    secret: true
required:
  - vault_server
  - vault_role_id
  - vault_secret_id
```
Injector configuration:
```yaml
extra_vars:
  ansible_hashi_vault_url: '{{ vault_server }}'
  ansible_hashi_vault_role_id: '{{ vault_role_id }}'
  ansible_hashi_vault_secret_id: '{{ vault_secret_id }}'
  ansible_hashi_vault_auth_method: approle
```
## Create new Credential
```yaml
Name: hashi_vault
Credential Type: Hashi vault
URL for Vault Server: https://<YOUR_VAULT_SERVER>
Role ID: role_id
Secret ID: secret_id
```
## Create new Inventory
Name: Vault-test

Variables:
```yaml
---
vault_test_var: "{{ lookup('community.hashi_vault.hashi_vault', 'secret=openshift/data/infra:test validate_certs=false') }}"
# read all values
#vault_test_var: "{{ lookup('community.hashi_vault.vault_read', 'openshift/data/infra', validate_certs=false) }}"
```
