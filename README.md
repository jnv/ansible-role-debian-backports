# Debian/Ubuntu Backports with Ansible

[![Ansible Role: jnv.debian-backports](https://img.shields.io/ansible/role/224.svg)](https://galaxy.ansible.com/jnv/debian-backports)
[![Build Status](https://github.com/jnv/ansible-role-debian-backports/workflows/Integration/badge.svg?branch=master)](https://github.com/jnv/ansible-role-debian-backports/actions?query=workflow%3AIntegration)

Adds backports repository for Debian and Ubuntu.

**Note for Debian users:** Debian provides backports [only for the latest stable version](https://backports.debian.org/news/stretch-backports/).

## Project Status

[![Project Status: Unsupported](https://www.repostatus.org/badges/latest/unsupported.svg)](https://www.repostatus.org/#unsupported)

The project has reached a stable, usable state but the author(s) have ceased all work on it. See [Similar Roles](#similar-roles) section for alternatives.

## Usage

Install via [Galaxy](https://galaxy.ansible.com/):

```
ansible-galaxy install jnv.debian-backports
```

In your playbook:

```yaml
- hosts: all
  roles:
    # ...
    - jnv.debian-backports
```

The role uses [apt_repository module](http://docs.ansible.com/apt_repository_module.html) which has additional requirements.

You can use `default_release` option for [apt module](http://docs.ansible.com/apt_module.html) to install package from backports. For example:

```yaml
tasks:
  - apt: name=mosh state=present default_release={{ansible_distribution_release}}-backports
```

`ansible_distribution_release` variable contains release name, i.e. `precise` or `wheezy`.

## Variables

- `backports_uri`: URI of the backports repository; change this if you want to use a particular mirror.
  - Debian: `https://deb.debian.org/debian`
  - Ubuntu: `http://archive.ubuntu.com/ubuntu`
- `backports_components`: Release and components for sources.list
  - Debian: `{{ backports_distribution }}-backports backports main contrib non-free`
  - Ubuntu: `{{ backports_distribution }}-backports main restricted universe multiverse`
- `backports_state`: Whether the backports repository should be used; default `'present'`, change to `'absent'` to disable the role.
- `backports_priority_enabled`: Whether to enable backports priority (APT pinning); default `false`.
- `backports_priority`: Set pin priority for the backports repository; default `100`. See more at [`AptConfiguration` page](https://wiki.debian.org/AptConfiguration).

## Similar Roles

- [jgeusebroek.backports](https://galaxy.ansible.com/jgeusebroek/backports)
- [oefenweb.apt](https://galaxy.ansible.com/oefenweb/apt) – does much more, but can be also used to enable backports.

## Testing

For developing and testing this role Github Actions, Molecule and Vagrant is used.
In a local environment environment you can easily test the role with

```
pip3 install molecule-vagrant ansible-lint yamllint
molecule test
```

This requires [Vagrant](https://www.vagrantup.com/downloads.html) to be installed.
