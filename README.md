# ansible-oracle

Ansible Collection `opitzconsulting.ansible_oracle` for the automated installation and management of Oracle Databases on Linux.

Start with one or more clean Linux hosts and end up with a fully configured Oracle database system:

* Single instance databases on filesystem or ASM
* Oracle Restart
* Oracle Real Application Clusters (RAC) and RAC One Node

**Documentation:** <https://www.ansible-oracle.eu>

## Features

* **Host preparation**: kernel parameters, users and groups, LVM, filesystems, swap, hugepages, firewall, ssh keys, cron and logrotate
* **Software installation**: Oracle Database, Oracle Restart and Grid Infrastructure, ASM (ASMFD, ASMlib, udev), AHF
* **Golden Images**: create and install Golden Images for RDBMS, Restart and Grid Infrastructure, read-only ORACLE_HOMEs
* **Patching**: download patches from My Oracle Support, in-place and out-of-place patching with OPatch/opatchauto, datapatch, timezone upgrades
* **Database management**: create databases with DBCA (CDB and non-CDB), PDBs, init.ora parameters, tablespaces, redo logs, users, roles, grants, profiles, services, wallets, Statspack, SQL*Net configuration
* **Backup**: RMAN with catalog, wallet and cron management
* **Oracle AutoUpgrade**: install AutoUpgrade, download Gold Images and patches, upgrade PDBs with Unplug/Plug from 19c to 26ai
* **APEX and ORDS**: installation and configuration
* **Modules**: `oracle_db`, `oracle_pdb`, `oracle_user`, `oracle_tablespace`, `oracle_sql`, ... based on `python-oracledb`

The complete list with supported versions is in the [feature list](https://github.com/oravirt/ansible-oracle/blob/master/doc/featurelist.adoc).

## Requirements

| Component | Supported versions |
|-----------|--------------------|
| ansible-core | 2.16 - 2.19 (`ansible-oracle` 4.x: 2.14 - 2.18) |
| Target OS | Oracle Linux / RHEL 8, 9, 10 |
| Oracle Database | 19c, 26ai |
| Oracle Restart / Grid Infrastructure | 19c |

> [!IMPORTANT]
> Oracle Linux / RHEL 8 ships Python 3.6 as system Python, which is not supported by ansible-core 2.17 or newer.
> Use ansible-core 2.16 for these hosts.

Collection dependencies are installed automatically from `galaxy.yml`:
`community.general` 11.x, `community.crypto` 2.x, `ansible.posix`, `ansible.utils` and `ibre5041.ansible_oracle_modules`.

## Installation

Install the collection from [Ansible Galaxy](https://galaxy.ansible.com/ui/repo/published/opitzconsulting/ansible_oracle/):

```shell
ansible-galaxy collection install opitzconsulting.ansible_oracle
```

or with a `requirements.yml`:

```yaml
---
collections:
  - name: opitzconsulting.ansible_oracle
    version: 4.17.0
```

```shell
ansible-galaxy collection install -r requirements.yml
```

## Usage

The collection contains ready-to-use playbooks. Import them in your own playbook and limit them to a host group with `hostgroup`:

```yaml
---
- name: Install a single instance database on filesystem
  ansible.builtin.import_playbook: opitzconsulting.ansible_oracle.single_instance_fs
  vars:
    hostgroup: dbfs
```

The configuration is done completely in the inventory (`host_vars`/`group_vars`).
Working examples are in [`example/`](https://github.com/oravirt/ansible-oracle/tree/master/example):

| Example | Description |
|---------|-------------|
| `beginner` | Oracle Database 26ai as single instance on filesystem with a Gold Image from AutoUpgrade |
| `beginner_patching` | Patching of the beginner setup |
| `rac` | Real Application Clusters with Vagrant |

### Playbooks

| Playbook | Description |
|----------|-------------|
| `os` | Prepare the host (OS configuration, storage, python-oracledb) |
| `swgi` | Install Oracle Restart / Grid Infrastructure and configure ASM |
| `swdb` | Install the Oracle Database software |
| `manage_db` | Create and configure databases, PDBs, tablespaces, users, ... |
| `single_instance_fs` | `os` + `swdb` + `manage_db` for a single instance on filesystem |
| `single-instance-asm` | `os` + `swgi` + `swdb` + `manage-db` for a single instance on ASM or Oracle Restart |
| `opatch` | Patch ORACLE_HOMEs and Grid Infrastructure |
| `patch_download` | Download patches from My Oracle Support |
| `golden_images` | Create Golden Images for Database and Restart |
| `autoupgrade_*` | Install AutoUpgrade, download patches, analyze/fixup/upgrade databases |
| `manage_ords`, `manage_sqlnet`, `manage_wallet` | ORDS, SQL*Net and wallet configuration |

The playbooks are called with the collection name, e.g. `opitzconsulting.ansible_oracle.swdb`.
All roles are listed in [doc/roles.adoc](https://github.com/oravirt/ansible-oracle/blob/master/doc/roles.adoc), each role has its own `README.md` with all variables.

## Documentation

The documentation is published at <https://www.ansible-oracle.eu>. The sources are in [`doc/`](https://github.com/oravirt/ansible-oracle/tree/master/doc):

* [Beginners Guide](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/beginner.adoc) - first installation step by step
* [Advanced Guide](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/advanced.adoc)
* [Oracle Restart and RAC](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/restart_rac.adoc)
* [Install and Patch Settings](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/Install-and-Patch-Settings.adoc)
* [Out-of-Place Patching](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/out_of_place_patching.adoc)
* [Oracle AutoUpgrade](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/autoupgrade.adoc)
* [Upgrade of PDBs with AutoUpgrade (Unplug/Plug)](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/autoupgrade_upgrade.adoc)
* [APEX and ORDS](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/apex_ords.adoc)
* [Vagrant setup on Windows](https://github.com/oravirt/ansible-oracle/blob/master/doc/vagrant.adoc)

## Upgrading

Major versions contain breaking changes in variables, defaults and supported versions.
Read the [Breaking Changes - Upgrade Guide](https://github.com/oravirt/ansible-oracle/blob/master/doc/guides/breaking_changes.adoc) before upgrading to a new major version.
All changes are listed in [CHANGELOG.rst](https://github.com/oravirt/ansible-oracle/blob/master/CHANGELOG.rst).

## Contributing

Contributions are welcome. Please read [How to develop in ansible-oracle](https://github.com/oravirt/ansible-oracle/blob/master/doc/development.adoc)
for the development environment (`nix-shell`), molecule tests, changelog fragments and pull requests.

Issues and pull requests: <https://github.com/oravirt/ansible-oracle>

## License

MIT, see [LICENSE](https://github.com/oravirt/ansible-oracle/blob/master/LICENSE).

## Authors

Mikael Sandström, Thorsten Bruhns and [OPITZ CONSULTING](https://www.opitz-consulting.com)
