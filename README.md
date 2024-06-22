# Consul cluster with Angie LB ansible playbook

### Inventory groups

* `angie_lb` Angie LB
* `consul_cluster` Consul nodes

### Angie LB vars

* `angie_repo_url` https://angie.software/installation/oss_packages/ for more info
* `angie_repo_gpg` https://angie.software/installation/oss_packages/ for more info
* `consul_ssl` use ssl (https) or not [true/false]

### Consul cluster vars

* `consul_version` distr version in semver https://github.com/hashicorp/consul/releases for more info
* `consul_zip_download_url` distr download url template (Hashicorp distr download url)
* `consul_datacenter` cluster dc name
* `consul_domain` cluster domain
* `consul_bind_address` by default uses `"{{ ansible_default_ipv4.address }}"` from gather facts, can be set to `0.0.0.0` for example
* `consul_user` user
* `consul_group` group
* `consul_bin_dir` bin path
* `consul_data_dir` data dir path
* `consul_config_dir` config dir path
* `consul_ca_path` path for CA cert
* `consul_cert_path` path for cert
* `consul_key_path` path for key
* `consul_binary_download` download and unpackage distr or skip download and unpackage task [true/false]
* `consul_cluster_helthcheck` perform helthcheck after cluster is up or skip helthcheck task [true/false]
* `consul_ui` enable or disable consul UI [true/false]
* `consul_ssl` use ssl (https) or not [true/false]
* `consul_acl` use acl or not [true/false]
* `consul_log_lvl` log level `"WARN"` by default

### How to

* setup inventory (there is `inventory.ini` example in repo)
* run `ansible-playbook -i inventory.ini play.yaml` from controller node

**INFO**

some examples of run playbook command

* `ansible-playbook -i inventory.ini play.yaml --ask-pass --ask-become-pass` to promt root password
* `ansible-playbook -i inventory.ini play.yaml --ask-pass --ask-become-pass --extra-vars "consul_version=1.18.2"` to promt root + become password and set var (downgrade Consul version for example)
* `ansible-playbook -i inventory.ini play.yaml --ask-pass --ask-become-pass --extra-vars '{"consul_binary_download": false, "consul_ssl": true}'` to promt root + become password and set boolean vars values in JSON format

**WARN**

if you whant to use `consul_ssl: true` - set it in global vars for all roles or in CLI command in JSON format, do not forget to add certs (ca.crt ssl.crt ssl.key) то `files/ssl` dir
