# Ansible Roles

Repo for storing ansible components and grouping them in roles to be reused in different projects.

More about ansible roles can be found at [Ansible's Docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html).

## Example

The following snippets show how to use the `git_updater` ansible role in a project.
```yaml
// requirements.yml 

---
roles:
  - src: git+https://github.com/wmde/ansible-roles.git
    version: main
    name: git_updater
```

```yaml
// setup.yml

- hosts: test_systems
  name: "Setup and run a test system for the 'WikibaseManifest' extension"
  become: yes
  vars:
    VECTOR_SUBPATH: "skins/Vector"
    ULS_SUBPATH: "extensions/UniversalLanguageSelector"
    CLDR_SUBPATH: "extensions/cldr"
    WIKIBASE_SUBPATH: "extensions/Wikibase"
    WIKIBASEMANIFEST_SUBPATH: "extensions/WikibaseManifest"
    OAUTH_SUBPATH: "extensions/OAuth"
  roles:
    - role: git_updater
      vars:
        git_directories:
          - "{{ MW_PATH }}"
          - "{{ MW_PATH }}/{{ VECTOR_SUBPATH }}"
          - "{{ MW_PATH }}/{{ ULS_SUBPATH }}"
          - "{{ MW_PATH }}/{{ CLDR_SUBPATH }}"
          - "{{ MW_PATH }}/{{ WIKIBASE_SUBPATH }}"
          - "{{ MW_PATH }}/{{ WIKIBASEMANIFEST_SUBPATH }}"
          - "{{ MW_PATH }}/{{ OAUTH_SUBPATH }}"
        USERNAME: mediawiki

```

:warning: You need to use ansible-galaxy to work with ansible roles.

```sh
$ ansible-galaxy install -r requirements.yml
$ ansible-playbook setup.yml --limit <hostname>.wikidata-dev.eqiad.wmflabs
```

### Example usage in WikibaseManifest
See: [WikibaseManifest Infrastructure Code](https://gerrit.wikimedia.org/r/plugins/gitiles/mediawiki/extensions/WikibaseManifest/+/refs/heads/master/infrastructure/) for somewhere this is used for WMDE test infrastructure.
