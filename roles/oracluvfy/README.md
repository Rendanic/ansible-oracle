# oracluvfy

Manage Cluster Verification Utility from Oracle

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [oracluvfy_archive](#oracluvfy_archive)
  - [oracluvfy_archive_filesource](#oracluvfy_archive_filesource)
  - [oracluvfy_executable](#oracluvfy_executable)
  - [oracluvfy_force_update](#oracluvfy_force_update)
  - [oracluvfy_home](#oracluvfy_home)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.14.0`

## Default Variables

### oracluvfy_archive

ZIP Archive used by the role.

#### Default value

```YAML
oracluvfy_archive: cvupack_linux_ol7_x86_64.zip
```

### oracluvfy_archive_filesource

If `oracluvfy_archive` ist not placed under `oracle_sw_source_local` / `oracle_sw_source_www`,
path can be forced using `oracluvfy_archive_filesource` instead.
`oracluvfy_archive_filesource` must be the full path/URL, including the filename.

#### Example usage

```YAML
oracluvfy_archive_filesource: /full/path/to/cvupack_linux_ol7_x86_64.zip
```

### oracluvfy_executable

Executable for cluvfy.

`oracluvfy_archive` is only installed, when `oracluvfy_executable` does not exist.
The default uses the cluvfy from `oracluvfy_archive`.
`runcluvfy.sh` from an unpacked Grid-Infrastructure home can be used as well.

#### Default value

```YAML
oracluvfy_executable: '{{ oracluvfy_home }}/bin/cluvfy'
```

#### Example usage

```YAML
oracluvfy_executable: "{{ oracle_home_gi }}/runcluvfy.sh"
```

### oracluvfy_force_update

Force unarchive of cluvfy in `oracluvfy_home`.

#### Default value

```YAML
oracluvfy_force_update: false
```

### oracluvfy_home

#### Default value

```YAML
oracluvfy_home: '{{ oracle_base }}/product/cluvfy'
```

## Discovered Tags

**_always_**

**_assert_**

## Dependencies

- orasw_meta

## License

license (MIT)

## Author

[Thorsten Bruhns]
