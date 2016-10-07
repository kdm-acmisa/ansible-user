## What is ansible-user? [![Build Status](https://secure.travis-ci.org/nickjj/ansible-user.png)](http://travis-ci.org/nickjj/ansible-user)

It is an [Ansible](http://www.ansible.com/home) role to:

- Create optional groups
- Create a user
- Copy over an SSH key to authorize logins
- Enable passwordless sudo

### What problem does it solve and why is it useful?

Often times you just want a single user created on a box with a few common tasks
taken care of for you.

ansible-user solves this by wrapping them together in 1 role so you don't have
to worry about the minutia of writing these tasks in every playbook.

## Role variables

```
---

# Optionally create and assign more groups than the default. If empty, users
# will automatically be a part of their user's group, ie. deploy/deploy.
user_groups: []

user_name: 'deploy'
user_shell: '/bin/bash'
user_enable_passwordless_sudo: True

# If you do not want SSH keys to be copied, use an empty string. Keep in mind
# if you do this, you won't be able to login!
user_local_ssh_key_path: '~/.ssh/id_rsa.pub'
```

If set, the local SSH key path will be transferred from your workstation to the
server(s) being provisioned.

## Example playbook

For the sake of this example let's assume you have a group called **app** and
you have a typical `site.yml` file.

To use this role edit your `site.yml` file to look something like this:

```
---

- name: Configure app server(s)
- hosts: app

  roles:
    - { role: nickjj.user, tags: user }
```

Let's say you want to edit the user name, you can do this by opening or
creating `group_vars/app.yml` which is located relative to your `inventory`
directory and then making it look something like this:

```
---

user_name: thor
```

## Installation

`$ ansible-galaxy install nickjj.user`

## Requirements

Tested on ubuntu 12.04 LTS but it should work on other versions that are similar.

## Ansible Galaxy

You can find it on the official
[Ansible Galaxy](https://galaxy.ansible.com/nickjj/user) if you want to
rate it.

## License

MIT
