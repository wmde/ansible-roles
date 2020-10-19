Role Name
=========

This role install a cronjob that repeatedly pulls the latest version of the master branch of git remote(s).

Role Variables
--------------

USERNAME: the user that should be running the update cronjob
SCRIPTS_DIR: where the update cronjob script should be saved
LOG_DIR: directory where logs from updating should go
git_repositories: which repositories should be updated.

Example Playbook
----------------

- hosts: test_systems
  name: "Setup and run a test system for the 'WikibaseManifest' extension"
  become: yes
  roles:
    - role: '/home/tom/src/wikimedia/wmde-ansible-roles/git-updater'
      vars:
        git_directories:
          - "/opt/Wikibase/src"

License
-------

BSD

Author Information
------------------

The Wikidata Team
