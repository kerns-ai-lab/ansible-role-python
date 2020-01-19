# Python Ansible Role

Installs Python, Python3 and related packages

## Requirements

This role requires Ansible 2.0 or higher.

## Role Variables

### Defaults

    - name: python2_install
      desc: Flag determining if python 2 should be installed
      default: True

    - name: python3_install
      desc: Flag determining if python 3 should be installed
      default: True

    - name: python3_version
      desc: Target python3 version to install (if not the default latest for distro)
      default: 3

    - name: python_pip_executable
      desc: Target pip executable to use for package installations (pip3 for python3 installs)
      default: pip3

    - name: python_pip_packages_extra
      desc: List of pip packages to install on top of base python packages required for development
      default: []

### Vars

These are not meant to be modified

    - name: python3_package
      desc: Target Python3 executable apt package
      value: "python{{ python3_version }}"

    - name: python2_packages
      desc: Python2 development packages
      value: 
      	- python
      	- python-dev
      	- python-pip

    - name: python3_packages
      desc: Python3 development packages
      value: 
      	- "{{ python3_package }}"
      	- python3-dev
      	- python3-pip

    - name: python_pip_packages
      desc: Python pip packages to install alongside base executable
      value: 
      	- virtualenv
      	- setuptools
      	- pipenv
      	- "{{ python_pip_packages_extra }}"

## Dependencies

None

## Example Playbook

Install Python2 & Python3

    - hosts: all
      roles:
        - ansible-role-python

Install Python2 only

    - hosts: all
      vars:
      	python3_install: False
      roles:
        - ansible-role-python

## Testing

Tests can be executed with local vagrantfile using the command. This mounts the role directory in the guest and executes the role via the playbook in `tests/` folder.

```shell
vagrant up
```