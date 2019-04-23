# Ansible console_perms role

This is an [Ansible](http://www.ansible.com) role which configures console permmissions.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Example Playbook

```yaml
---

- hosts: all
  roles:    
    - role: amtega.console_perms
    vars:
      console_perms:
        - path: /etc/security/console.perms
          classes:
            - name: console
              files:
                - 'tty[0-9][0-9]*'
                - 'vc/[0-9][0-9]*'
                - ':[0-9]+\.[0-9]+'
                - ':[0-9]+'
            - name: xconsole
              files:
                - ':[0-9]+\.[0-9]+'
                - ':[0-9]+'
          # permissions:
        - path: /etc/security/console.perms.d/51-default.perms
          classes:
            - name: floppy
              files:
                - /dev/fd[0-1]*
                - /dev/floppy/*
                - /mnt/floppy*
            - name: sound
              files: ['/dev/dsp*', '/dev/audio*', '/dev/midi*', '/dev/mixer*', '/dev/sequencer', '/dev/sound/*', '/dev/beep', '/dev/snd/*']
            - name: cdrom
              files: ['/dev/cdrom*', '/dev/cdroms/*', '/dev/cdwriter*', '/mnt/cdrom*']
            - name: scanner
              files: ['/dev/scanner', '/dev/usb/scanner*']
          permissions:
            - class: <console>
              class_perm: '0660'
              device: <floppy>
              revert_mode: 0660
              revert_owner: root
              revert_group: floppy
            - class: <console>
              class_perm: '0660'
              device: <sound>
              revert_mode: 0640
              revert_owner: root
            - class: <console>
              class_perm: '0660'
              device: <cdrom>
              revert_mode: 0660
              revert_owner: root
              revert_group: disk

```

## Testing

<!-- A description of how to run tests of the role if available. For example: -->

Tests are based on docker containers. You can setup docker engine quickly using the playbook `files/setup.yml` available in the role [amtega.docker_engine](https://galaxy.ansible.com/amtega/docker_engine).

Once you have docker, you can run the tests with the following commands:

```shell
$ cd amtega.console_perms/tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2019 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify
it under the terms of:
GNU General Public License version 3, or (at your option) any later version;
or the European Union Public License, either Version 1.2 or – as soon
they will be approved by the European Commission ­subsequent versions of
the EUPL;

This role is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas
