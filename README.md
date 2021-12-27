# ansible-role-hashicorp

An ansible role to install the following HashiCorp products

- Consul
- Nomad
- Terraform
- Vault

## Requirements

None.

## Role Variables

None.

## Dependencies

None.

## Example Playbook

    - hosts: servers
      become: true
      roles:
         - { role: chrisvanmeer.hashicorp }

## License

MIT
