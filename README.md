# ferm-deploy

This role installs `ferm` and `ipset` and copies a folder containing ferm configuration files to `/etc/ferm`.


## Requirements

This is tested on Debian but should also work on its derivates.
`files/ferm` should exist and contain at least a `ferm.conf` file.


## Role Variables

| Name                | Required/Default | Description                                               |
|---------------------|:----------------:|-----------------------------------------------------------|
| `ferm_deploy_group` | `root`           | Group that should own the ferm files touched by this role |


## Example

```yml
ferm_deploy_group: adm
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Michel Weitbrecht (SlothOfAnarchy)](https://github.com/SlothOfAnarchy) _michel.weitbrecht@stuvus.uni-stuttgart.de_
