# oraswords_meta


Meta role used by other roles to share variable defaults

This role is needed for _oraswords_install_.

This role has a dependency to `orahost_meta`.

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [oraswords_meta_db_pools](#oraswords_meta_db_pools)
  - [oraswords_meta_oracle_home](#oraswords_meta_oracle_home)
  - [oraswords_meta_ords_config](#oraswords_meta_ords_config)
  - [oraswords_meta_ords_logs](#oraswords_meta_ords_logs)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.14.0`

## Default Variables

### oraswords_meta_db_pools

List of configured target in ORDS.

Attributes:

db_pool: <Pool in ORDS>

pdb_name: <Target PDB. Needed to find the Password s>

port: <Listener Port>

service: <servicename of target. Defaults to pdb_name>

hostname: <Hostname for target. Defaults to `inventory_hostname`>

#### Default value

```YAML
oraswords_meta_db_pools:
  - db_pool: default
    pdb_name: orclpdb
    admin_user: sys
    service: orclpdb
    port: 1521
```

### oraswords_meta_oracle_home

`ORACLE_HOME` for _ORDS_.

#### Default value

```YAML
oraswords_meta_oracle_home: >-
  {{ oracle_base }}/product/ords
```

### oraswords_meta_ords_config

#### Default value

```YAML
oraswords_meta_ords_config: >-
  /etc/ords/config
```

### oraswords_meta_ords_logs

#### Default value

```YAML
oraswords_meta_ords_logs: >-
  /etc/ords/logs
```

## Discovered Tags

**_always_**

**_assert_ansible_oracle_**


## Dependencies

None.

## License

license (MIT)

## Author

[Thorsten Bruhns]
