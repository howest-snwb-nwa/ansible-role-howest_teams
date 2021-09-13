Role Name
=========

An Ansible Role that:
* Adds channels to a team you own
* Adds users to a team you own, based on LEHO(Canvas) information.

Teachers will be Team **owner** and students will be guests.

Requirements
------------

This role is meant to run on your own machine (localhost).

How to Run
----------
 
1. `git clone https://github.com/howest-snwb-nwa/ansible-role-howest_teams.git` to your Ansible roles directory
2. Rename to howest_teams as given in the playbook below. Make a playbook with the right variables. For TI, this is an example (`howest_teams_TI.yaml`):
    ```  
    ---
    # Create channels and sync users.
    - name: HOWEST - create Teams channels and sync users from LEHO.
      hosts: localhost
      gather_facts: false
      vars_files:
        - ~/ansible/vars/api_keys.yml   # Voor access tokens (ansible-vault).
      vars:
        leho_course_infosite: 10990   # Wijzig naar infosite TI 2021-2022!
        team_displayname: STUDENT.TI.21-22
        team_channels:
          - General
        # api_key_leho: indien niet in vars_files
        # api_key_ms: indien niet in vars_files
      roles:
        - howest_teams
    ```

    * More channels can be added.
    * Already existing users are checked. That's the reason why the ms graph API calls use the beta URL. The stable 1.0 is bugged (oh, the irony).
    * The playbook is idempotent: run as many times as you want.
    * Test what will happen with `--check`
    * Adding only channels or members: use `--tags channel` or `--tag member`. This won't be time saving.


Role Variables
--------------

* `api_key_leho`: Your Canvas access token. To create one, in Canvas, go to Settings > New access token.
* `api_key_ms`: Your Microsoft Graph access token. See https://docs.microsoft.com/en-us/graph/auth/
* `team_displayname`: The Team name as seen in Microsoft Teams.
* `leho_course_infosite`: The id of the LEHO module. This can be found in the URL of the module.
* `team_channels`: A list of channels to be added. If you leave this variable empty or undefined, no channels will be added.

Dependencies
------------

None.

Example Playbook
----------------

Get users from the SNWB Infosite and add them to Microsoft Teams.

```YAML
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
