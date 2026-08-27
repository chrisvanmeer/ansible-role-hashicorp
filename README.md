# ansible-role-hashicorp

An Ansible role to install the following HashiCorp products from HashiCorp's
official package repositories:

- Boundary
- Consul
- Nomad
- Packer
- Terraform
- Vagrant
- Vault

No configuration on the products is done. This is just an install through
the distribution's package manager (`apt` or `dnf`), with an optional pinned
version per product.

**Nothing is installed by default.** You must explicitly list the products
you want via `hashicorp_products`.

## Requirements

- Ansible >= 2.14
- A supported target OS (see below)

## Continuous integration

Every push triggers two GitHub Actions workflows:

- `.github/workflows/lint.yml` runs `yamllint` and `ansible-lint` (production
  profile) against the role.
- `.github/workflows/functional-test.yml` actually runs the example
  playbook shown above (`tests/test.yml`) inside real Ubuntu 26.04,
  Debian 13, Fedora, Rocky Linux 10 and AlmaLinux 10 containers, then
  verifies that `terraform`, `vault` and `consul` were genuinely installed
  (including the pinned versions) by executing their `version` commands.

## Supported platforms

| OS family   | Distributions                             |
| ----------- | ----------------------------------------- |
| Debian      | Debian, Ubuntu                            |
| RedHat (EL) | RHEL, CentOS, Rocky Linux, AlmaLinux (8+) |
| Fedora      | Fedora                                    |

Other operating systems will cause the role to fail with a clear error
message instead of silently doing nothing.

Internally, the role picks its OS-specific variables (which in turn select
the task file to run) using an Ansible `first_found` lookup, checked in this
order:

1. `vars/<distribution>-<major_version>.yml` (e.g. `vars/RedHat-9.yml`)
2. `vars/<distribution>.yml` (e.g. `vars/Fedora.yml`)
3. `vars/<os_family>.yml` (e.g. `vars/Debian.yml`, `vars/RedHat.yml`)

This makes it straightforward to add a distribution- or version-specific
override later (for example a different repository URL for a single EL
major version) without touching the generic task logic.

## Role Variables

Available variables are listed below, along with default values (see
`defaults/main.yml`):

```yaml
hashicorp_products: []
```

`hashicorp_products` is a list of dicts. Each item requires a `name` and
accepts an optional `version`:

```yaml
hashicorp_products:
  - name: terraform
    version: "1.7.5"   # pin an exact upstream version
  - name: vault
    version: "1.15.6"
  - name: consul        # no version -> latest available is installed
```

Valid values for `name` are: `boundary`, `consul`, `nomad`, `packer`,
`terraform`, `vagrant`, `vault`. Any other value, or a missing
`name` key, makes the role fail fast with an assertion error rather than
continuing with a typo.

Version pinning is passed through to the underlying package manager
(`name=version*` on APT, `name-version*` on DNF), so use the upstream
product version (e.g. `1.7.5`), not the full Debian/RPM package revision.
If the requested version is not available in HashiCorp's repository for
your distribution, the task fails with the package manager's own error.

Other variables you generally won't need to touch:

```yaml
hashicorp_apt_keyring_dir: /usr/share/keyrings
hashicorp_apt_keyring_path: "{{ hashicorp_apt_keyring_dir }}/hashicorp-archive-keyring.gpg"
hashicorp_gpg_key_url: https://apt.releases.hashicorp.com/gpg
```

## Dependencies

No dependencies.

## Installation

Install this role with the following command:

```bash
ansible-galaxy install chrisvanmeer.hashicorp
```

## Example Playbook

```yaml
- hosts: servers
  become: true

  vars:
    hashicorp_products:
      - name: terraform
        version: "1.15.8"
      - name: vault
        version: "2.0.4"
      - name: consul
        version: "2.0.3"

  roles:
    - role: chrisvanmeer.hashicorp
```

Note: Vault and Consul moved to a `2.x` versioning scheme in 2026; Terraform is
still on the `1.x` line. Check each product's release notes for the current
version before pinning it in production.

## License

MIT
