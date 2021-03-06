# ansible-role-auter

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-auter.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-auter)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-auter-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/auter)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Automatic updates for RHEL, CentOS or Fedora Linux servers

## Requirements

This role requires that you have the epel repository installed.

 * https://galaxy.ansible.com/linuxhq/epel/

## Role Variables

Available variables are listed below, along with default values:

    auter_autoreboot: false
    auter_configset: default
    auter_cronjobs: []
    auter_maxdelay: 3600
    auter_onlyinstallfromprep: false
    auter_packagemanageroptions: ''
    auter_postapplyscriptdir: /etc/auter/post-apply.d
    auter_postapplyscripts: []
    auter_postrebootscriptdir: /etc/auter/post-reboot.d
    auter_postrebootscripts: []
    auter_preapplyscriptdir: /etc/auter/pre-apply.d
    auter_preapplyscripts: []
    auter_predownloadupdates: true
    auter_prerebootscriptdir: /etc/auter/pre-reboot.d
    auter_prerebootscripts: []

## Dependencies

None
 
## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.auter
          auter_onlyinstallfromprep: true
          auter_cronjobs:
            - name: Pre-download updates before applying
              job: /usr/bin/auter --prep
              minute: 0
              hour: 05
              weekday: '*'
              day: '*'
              month: '*'
            - name: Apply updates, and reboot if AUTOREBOOT=yes
              job: /usr/bin/auter --apply
              minute: 0
              hour: 06
              weekday: '*'
              day: '*'
              month: '*'
          auter_preapplyscripts:
            - name: pre_apply.sh
              mode: 700
              base64: |
                ZWNobyBwcmVfYXBwbHkK
          auter_postapplyscripts:
            - name: post_apply.sh
              mode: 700
              base64: |
                ZWNobyBwb3N0X2FwcGx5Cg==

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
