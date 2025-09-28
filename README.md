# Ansible Signal

An Ansible role for installing the Linux desktop client for [Signal](https://signal.org)

---

### Requirements

This role requires the `ansible.utils` collection be installed from Ansible-Galaxy via:

```shell
ansible-galaxy collection install ansible.utils
```

It then also requires the `jsonschema` Python package be installed. It can be installed via pip:

```shell
pip3 install jsonschema
```

### Role Variables

This role requires the following input variables:

```yaml
signal:
  remove: [bool]              Indicates if the application should be removed. Also removes repository information.
  gather_facts: [bool]        Indicates if package fact action should be gathered before going through configuration steps. Defaults to true.
  signing:
    ascii_key_file: [string]  [required] Path to the public ascii signing key that Signal signs their packages with.
```

#### Signing key

Signal hosts their signing key over at https://updates.signal.org/desktop/apt/keys.asc

### Setup


Before the role can be used it needs to be added to the machine running the playbook, and as of writing this, this role is not hosted on Ansible-Galaxy only on Github.

1. Create a `requirements.yml` file in the root directory of the playbook being worked on.

2. Add the following definition inside the `requirements.yml` file:

```yml
- name: hth-act
  src: https://github.com/hrafnthor/ansible-signal.git
  scm: git
```

3. Install the requirements by executing

```shell
ansible-galaxy install -r .requirements.yml
```

This will allow any playbook run from this machine to use the role `hth-signal`


### Example input

```yaml
signal:
  remove: false
  gather_facts: false
  signing:
    ascii_key_file: signal-desktop-signing-key.asc
```

### Example playbook

```yaml
- hosts: all
    vars:
    - signal:
      remove: false
      gather_facts: false
      signing:
        ascii_key_file: signal-desktop-signing-key.asc
  roles:
  - hth-signal
```



## License

Apache 2.0. See attached license file.

## Author Information

Hrafn Thorvaldsson.
http://www.hth.is
