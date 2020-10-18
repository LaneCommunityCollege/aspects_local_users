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
  vars:
    aspects_local_users_enabled: True
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
        uid: 10006
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
        gid: 2005
    aspects_local_users_system_users:
      sysaspects:
        state: "present"
        username: "sysaspects"
        fullname: "test system user"
        crypted_pass: '$6$password123$MtblzP5ivc0dWizVaOhUlpwwIQggaPwq2Fjjz19Ef1mcxUMVRvpxg0M.Hp.l5bvbQY7zwH9piocaOa0K9mOkW.'
        shell: "/bin/bash"
        uid: 444
      sysbeta:
        state: "absent"
        username: "sysbeta"
        fullname: "beta system user"
        crypted_pass: '$6$password123$MtblzP5ivc0dWizVaOhUlpwwIQggaPwq2Fjjz19Ef1mcxUMVRvpxg0M.Hp.l5bvbQY7zwH9piocaOa0K9mOkW.'
        home: "/opt/sysbeta"
        group: "mail"
        shell: "/bin/bash"
        uid: 445
    aspects_local_users_system_groups:
      alpha:
        state: "present"
        name: "alpha"
        gid: "333"
      beta:
        state: "absent"
        name: "alpha"
        gid: "334"
  roles:
     - aspects_local_users
```
# License
MIT
