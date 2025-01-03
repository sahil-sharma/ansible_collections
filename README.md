# Ansible Collection - task.automation

# My Collection

This collection contains two roles:

1. **local_accounts**: Creates multiple local user accounts with configurable properties and enables passwordless login.
2. **ssh_config**: Configures SSH daemon options for secure authentication.

## Roles
- `local_accounts`: Create local user accounts.
- `ssh_config`: Configures the SSH daemon with specific settings.

## Usage Example

```yaml
- name: Apply local user creation and SSH configuration
  hosts: all
  become: yes
  roles:
    - task.automation.local_accounts
    - task.automation.ssh_config
```

Set the collection path and run the playbook:

```bash
export ANSIBLE_COLLECTIONS_PATHS=/vagrant/ansible_collections
cd /vagrant/ansible_collections/task/automation

# CheckMode allows you to simulate the execution of a playbook without making any actual changes to the target systems
ansible-playbook -i inventory/hosts.yml playbooks/apply_roles.yml --check

# Without CheckMode (no --dry-run)
ansible-playbook -i inventory/hosts.yml playbooks/apply_roles.yml
```

## Build Your Collection

You need to package your collection into a .tar.gz file using the ansible-galaxy CLI.

Open a terminal and navigate to the root of your collection directory (the directory that contains your galaxy.yml file).
Run the following command to create the collection package:
```shell
ansible-galaxy collection build
```

This will generate a .tar.gz file in the current directory, such as:
```shell
test-automation-1.0.0.tar.gz
```

## Login to Ansible Galaxy

Before uploading, you need to authenticate your local machine with Ansible Galaxy. Use the following command to log in:
```shell
ansible-galaxy login
```
This command will prompt you for your Galaxy credentials (username and password).

## Upload the Collection to Ansible Galaxy

Once logged in, use the following command to upload the collection to Ansible Galaxy:
```shell
ansible-galaxy collection publish test-automation-1.0.0.tar.gz
```
