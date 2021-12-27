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

######product_selection
This variable can be changed to match your prefference.  
Defaults to:

```
product_selection:
  - consul
  - nomad
  - terraform
  - vault
```

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

  vars:
    product_selection:
      - consul
      - nomad
      - terraform
      - vault

  roles:
    - role: chrisvanmeer.hashicorp
```

## License

MIT
