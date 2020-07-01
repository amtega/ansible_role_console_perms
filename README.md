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
        - path: /etc/security/console.perms.d/51-default.perms
          classes:
            - name: floppy
              files:
                - /dev/fd[0-1]*
                - /dev/floppy/*
                - /mnt/floppy*
            - name: sound
              files:
                - /dev/dsp*
                - /dev/audio*
                - /dev/midi*
                - /dev/mixer*
                - /dev/sequencer
                - /dev/sound/*
                - /dev/beep
                - /dev/snd/*
            - name: cdrom
              files:
                - /dev/cdrom*
                - /dev/cdroms/*
                - /dev/cdwriter*
                - /mnt/cdrom*
            - name: scanner
              files: -
                - /dev/scanner
                - /dev/usb/scanner*
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

Tests are based on [molecule with docker containers](https://molecule.readthedocs.io/en/latest/installation.html).

```shell
cd amtega.console_perms

molecule test --all
```

## License

Copyright (C) 2020 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas
