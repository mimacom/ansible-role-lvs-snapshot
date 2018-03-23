# Ansible Role: lvs-snapshot

[![Build Status](https://travis-ci.org/mimacom/ansible-role-lvs-snapshot.svg?branch=master)](https://travis-ci.org/mimacom/ansible-role-lvs-snapshot)

Installs a cronjob which creates a snapshot of a Logical Volume (using Logical Volume Manager). In addition, all running Docker container will be paused while the snapshot is taken.

## Requirements

You need LVM and Docker installed on your system. This role will not install it for you (yet).

## Role Variables

Available variables are listed below, along with default values (see
`defaults/main.yml`):

    lvssnap_creation_time: []

Dictionary which accepts `hour` and `minute` when to take the snapshot.

    lvssnap_deletion_time: []

Dictionary which accepts `hour` and `minute` when to delete the snapshot.

    lvssnap_lv_device: ""

Path to the LV device to snapshot.

    lvssnap_snapshot_device: ""

Path to the snapshot LV device to create.

    lvssnap_snapshot_mountpoint: ""

Path where to mount the snapshot to.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      become: yes
      vars:
        lvssnap_creation_time:
          hour: 21
          minute: 50
        lvssnap_deletion_time:
          hour: 4
          minute: 0
        lvssnap_lv_device: /dev/data/docker
        lvssnap_snapshot_device: /dev/data/docker_snap
        lvssnap_snapshot_mountpoint: /media/docker_snap
      roles:
        - role: mimacom.lvs-snapshot

## License

Apache License 2.0

## Author Information

This role was created by [Remo Wenger](http://www.remowenger.ch) of [mimacom ag](https://www.mimacom.com/).
