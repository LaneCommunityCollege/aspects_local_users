# aspects_local_users

Manage local linux users. 

# Requirements

Set ```hash_behaviour=merge``` in your ansible.cfg file.

# Role Variables
## aspects_local_users
Dictionary of users. See the Example Playbook for more.

## aspects_local_users_ssh_keys
The public keys you want to add to various users. See the Example Playbook for more.

# Example Playbook

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
        aspects_local_users_ssh_keys:
          webby:
            state: present
            username: webby
            ssh_pubkey: 'first pub key'
          webby2:
            state: present
            username: webby
            ssh_pubkey: 'second pub key'

# License
MIT
