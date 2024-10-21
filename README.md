# Ansible Role: GitHub Users

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

Create users based on GitHub accounts.

This role will take a GitHub username and create a system account with the same username, and will add all the pubkeys associated with the GitHub account to the user's `authorized_keys`.

It's kind of a cheap way to do public key management for users on your system... but it works!

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    github_users: []
      # You can specify an object with 'name' (required) and 'groups' (optional):
      # - name: nholuong
      #   groups: www-data,sudo
    
      # Or you can specify a GitHub username directly:
      # - nholuong

A list of users to add to the server; the username will be the `name` (or the bare list item, if it's a string instead of an object). You can add the user to one or more groups (in addition to the `[username]` group) by adding them as a comma-separated list in `groups`.

    github_users_absent: []
      # You can specify an object with 'name' (required):
      # - name: nholuong
    
      # Or you can specify a GitHub username directly:
      # - nholuong

A list of users who should _not_ be present on the server. The role will ensure these user accounts are removed.

    github_users_authorized_keys_exclusive: true

Whether the users' `authorized_keys` files should exclusively contain keys from their GitHub account. This should normally be set to `true` if you are only allowing users to log in using keys available in their GitHub accounts.

    github_url: https://github.com

By default, use public GitHub (i.e. https://github.com) as the source for users/keys. Override this to use a different GitHub instance/endpoint (e.g. GitHub Enterprise).

If you need to give the user the ability to self-manage their `authorized_keys` file, then you should set this to `no`, and it will only append new keys, but never remove any additional keys (e.g. old keys removed from their GitHub profile, or keys the end user added manually) from the file.

## Dependencies

None.

## Example Playbook

    - hosts: servers
    
      vars:
        github_users:
          # You can specify the `name`:
          - name: nholuong
            groups: sudo,www-data
          - name: GrahamCampbell
          # Or if you don't need to override anything, you can specify the
          # GitHub username directly:
          - fabpot
    
        github_users_absent:
          - nholuong
          - name: nho
    
      roles:
        - nholuong.github-users

If you want to make sure users' public keys are in sync, it is best to run the playbook on a cron, e.g. every 5 min, 10 min, or some other interval. That way you don't have to manually add new keys for users.

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟