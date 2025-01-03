local_accounts
=========
This role creates local user accounts as per the given configurations.

Role Variables
--------------
- `users`: List of dictionaries where each dictionary contains user information like name, shell, uid, home directory, groups, and expiry date.

Example Playbook
----------------
Example:

```yaml
users:
  - name: "user1"
    userid: 1001
    home: "/home/user1"
    shell: "/bin/bash"
    expiry_date:
    groups: []

  - name: "user2"
    userid: 1002
    home: "/home/user1"
    shell: "/bin/sh"
    expiry_date: "2025-12-31"
    groups: []