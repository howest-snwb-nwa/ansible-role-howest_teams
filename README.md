Role Name
=========

An Ansible Role that:
* Adds channels to a team you own
* Adds users to a team you own, based on LEHO(Canvas) information.

Teachers will be Team **owner** and students will be guests.

Requirements
------------

This role is meant to run on your own machine (localhost).

Role Variables
--------------

* `api_key_leho`: Your Canvas access token. To create one, in Canvas, go to Settings > New access token.
* `api_key_ms`: Your Microsoft Graph access token. See https://docs.microsoft.com/en-us/graph/auth/
* `team_displayname`: The Team name as seen in Microsoft Teams.
* `leho_course_infosite`: The id of the LEHO module. This can be found in the URL of the module.
* `team_channels`: A list of channels to be added.

Dependencies
------------

None.


Example Playbook
----------------

Get users from the SNWB Infosite and add them to Microsoft Teams.

```
- name: HOWEST - create Teams channels and sync users from LEHO.
  hosts: localhost
  gather_facts: false
  vars:
    api_key_leho: your-leho-api-key
    api_key_ms: your_msgraph-access-token
    leho_course_infosite: 14651
    team_displayname: STUDENT.SNWB.21-22.JH1
    
  roles:
    - howest_teams
```

License
-------

BSD

Author Information
------------------

This role was created in 2021 by Alvin Demeyer for [Howest](https://www.howest.be/).
