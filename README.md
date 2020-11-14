# ferm-deploy

This role installs `ferm` and `ipset` and allows to copy ferm configuration files to the machine.


## Requirements

This is tested on Debian but should also work on its derivates.

## Role Variables

| Name                                |         Required/Default          | Description                                                                                                                                                                                                                                |
| ----------------------------------- | :-------------------------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `ferm_deploy_config_files_defaults` | See [defaults](defaults/main.yml) | Default flags given to the copy module when copying the config files.                                                                                                                                                                      |
| `ferm_deploy_configs`               | See [defaults](defaults/main.yml) | A list of ferm config files to be put on the host. Each item should be a dict containing the keys and values as expected by the copy module. Any values not specified in that dict will be taken from `ferm_deploy_config_files_defaults`. |


## Examples
For the most simple case no variable needs to be set.
Then the folder `ferm` in the files directory of the playbook will be copied to `/etc/ferm` on the host.

If the files to be copied and the file attributes for them need to be customized the config could look like that:
```yml
ferm_deploy_config_files_defaults: 
  mode: 0644
  directory_mode: 0755
  owner: root
  group: network
ferm_deploy_configs:
  - dest: /etc/ferm/ferm.conf
    src: ferm/ferm.conf
  - dest: /etc/ferm/someOtherFile.conf
    src: ferm/someOtherFile.conf
  - dest: /etc/ferm/someFolder
    src: ferm/someFolder/
```

It is also possible to specify the content within a file:
```yml
ferm_deploy_configs:
  - dest: /etc/ferm/ferm.conf
    content: |
      domain ip chain INPUT {
        mod state state INVALID DROP;
        mod state state (ESTABLISHED RELATED) ACCEPT;
        proto tcp dport 22 ACCEPT;
        DROP;
      }
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

- [Michel Weitbrecht (SlothOfAnarchy)](https://github.com/SlothOfAnarchy) _michel.weitbrecht@stuvus.uni-stuttgart.de_
- [Tim Neumann (neumantm)](https://github.com/neumantm) _tim.neumann@stuvus.uni-stuttgart.de_
