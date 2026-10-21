# N8n ansible role
A simple ansible role to set a n8n community edition on a debian virtual machine with external postgresql and python runner. Include a reverse proxy httpd used for control access and authentication (openid connect).

## Usage
Configure n8n instance (require):
- `n8n_version`: targeted n8n release (https://github.com/n8n-io/n8n/tags)
- `n8n_dir`: local directory contains docker-compose files
- `n8n_fqdn`: name of this instance used in webui url (if you dont have fqdn, you can use /etc/hosys on your computer)

Setting up database (require):
- `n8n_db_host`: psql fqdn or ip address
- `n8n_db_name`: pgsql database name (not schema)
- `n8n_db_user`: pgsql user (dont forget config pg\_hba.conf)
- `n8n_db_pass`: pgsql user's password (encrypt with ansible vault)

Configure python runner (require):
- `n8n_runner_token`: 
- `n8n_runner_python_import`: list of python modules to import (for example "dnspython")

Setting openid connect on relying party (optionnal):
- `n8n_oidc_enabled`: Enable reverse proxy httpd OIDC
- `n8n_oidc_provider_url`: OIDC metadata url on OIDC provider (this url generally end with /.well-known/openid-configuration)
- `n8n_oidc_client_id`: RP id
- `n8n_oidc_client_secret`: secret associated with RP id
- `n8n_oidc_session_secret`: passphrase used to ecrypt cookie
- `n8n_oidc_users_root`: list of sub claims authorize to access n8n webUI

Recommanded : Using a local firewall like firewalld on virtual machine. Example ansible role :
https://github.com/ggambini/simple-firewalld-ansible-role

## Inventory and playbook
Simùply call n8n role with your others roles :
```
- name: Deploy SOAR n8n nodes
  hosts: soar-app

  roles:
    - simple-firewalld-ansible-role
    - n8n-role
```

## License
AGPLv3

## Author Information
Gilian GAMBINI @ INRAE-SSI-COS
