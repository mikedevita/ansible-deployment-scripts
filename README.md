# ansible Deployment Script
Sets up servers with some basic configurations

1. Runs apt-update and installs `vim, htop, git, curl, ncdu, tmux, zsh` packages
1. Locks SSH password bsed authentication
1. Creates a new `user`, with provided details
1. Sets the timezone to the provided `timezone`
1. Disallow root password SSH access

## Prerequisites
1 . You need to be able to login to the remote servers via root without a password.

* Ensure that the `ssh_pub_key` is added to the `root` users `/root/.ssh/authorized_keys` file

## Installation

1. Clone this repository `git clone git@github.com:mikedevita/ansible-deployment-scripts`
2. Update the `hosts` file with the correct server hostnames or ip addresses
3. Update the vault file or create it with the required parameters

## Parameters

| Key | Required | Default Value | Description |
|---|---|---|--|
| ssh_pub_key | Yes |  | SSH Public Key that is used to login to run the ansible scripts, this should be in the root users `authorized_keys` file
| user_name | No | 'mike' | Username of new user thats to be created |
| user_uid | No | 1000 | User id of the new user thats to be created | 
| user_groups | No | ['sudo', 'mike'] | array of groups the new user will belong to
| user_shell | No | '/usr/bin/zsh' | What shell the new user will have
| user_groups_append | No | yes | Yes or no on whether to append the user_groups to the existing
| user_home | No | '/home/mike' | The home directory path for the new user
| user_ssh_key | No | '~/.ssh/id_rsa.pub' | SSH Public key that the will be added to the new users `authorized_keys` file
| timezone | No | 'America/Phoenix' | Timezone the server is to set to


## Running
1. To run with a vault file: `ansible-playbook playbook.yml --ask-vault-pass -i hosts`
1. To run without a vault file: `ansible-playbook -i hosts playbook.yml`
1. To create a new vault file: `ansible-vault create vault.yml`
1. To edit the existing vault file: `ansible-vault edit vault.yml`