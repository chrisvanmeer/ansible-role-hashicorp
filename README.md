# ansible-role-hashicorp

An ansible role to install the following HashiCorp products

- Consul
- Nomad
- Terraform
- Vault

No configuration on the products is done. This is just the vanilla install through the distri's package manager.

## Requirements

None.

## Role Variables

None.

## Dependencies

None.

## Installation

Install this role with the following command:

```
ansible-galaxy install chrisvanmeer.hashicorp
```

## Example Playbook

```
- hosts: servers
  become: true
  roles:
    - { role: chrisvanmeer.hashicorp }
```

## License

MIT
