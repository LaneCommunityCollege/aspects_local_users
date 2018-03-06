# aspects_local_users

Manage local Linux user accounts, groups, and user authorized ssh keys.

# Requirements

Set ```hash_behaviour=merge``` in your ansible.cfg file.

# Role Variables
## aspects_local_users_enabled
To enable or disable this role. Set to True to enable. False to disable.

Default is `False`

## aspects_local_users
Dictionary of users. See the Example Playbook for more.

## aspects_local_users_groups
Dictionary of extra groups.

```yaml
aspects_local_users_groups:
  <keyidentifier>:
    state: <present|absent>
    name: <name of the group>
    gid: <gid of the group>
```

## aspects_local_users_ssh_keys
The public keys you want to add to various users. See the Example Playbook for more.

# Example Playbook
```yaml
- hosts: servers
  roles:
     - aspects_local_users
  vars:
    aspects_local_users:
      webserveruser:
        state: present
        username: webby
        fullname: Web By
        crypted_pass: 'thepasswordgoeshere'
        shell: /bin/bash
        groups:
          Debian: "www-data"
          RedHat: "apache"
        uid: 10005
      optuser:
        state: present
        username: opter
        fullname: Opt By
        crypted_pass: 'thepasswordgoeshere'
        home: /opt/opterdir
        shell: /bin/bash
        groups:
          Debian: "www-data"
          RedHat: "apache"
        uid: 10005
    aspects_local_users_ssh_keys:
      webby:
        state: present
        username: webby
        ssh_pubkey: 'first pub key' # Note that the authorized_key module appears to validate this, so the example value here will fail.
      webby2:
        state: present
        username: webby
        ssh_pubkey: 'second pub key' # Note that the authorized_key module appears to validate this, so the example value here will fail.
    aspects_local_users_groups:
      webusers:
        state: present
        name: webusers
        gid: 11111
      oldwebusers:
        state: absent
        name: webserverusers
        gid: 1005
```
# License
MIT
