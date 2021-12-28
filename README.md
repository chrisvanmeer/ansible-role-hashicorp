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

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th width="150px">Default Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr valign="top">
      <td>hashicorp_product_selection</td>
      <td>
        <ul>
          <li>consul</li>
          <li>nomad</li>
          <li>terraform</li>
          <li>vault</li>
        </ul>
      </td>
      <td>Allows for a subselection of products to be installed. Defaults to the whole suite.</td>
    </td>
  </tbody>
</table>

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
    hashicorp_product_selection:
      - consul
      - nomad
      - terraform
      - vault

  roles:
    - role: chrisvanmeer.hashicorp
```

## License

MIT
