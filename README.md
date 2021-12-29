# ansible-role-hashicorp

An ansible role to install the following HashiCorp products

- Boundary
- Consul
- Nomad
- Packer
- Terraform
- Vagrant
- Vault
- Waypoint

No configuration on the products is done. This is just the vanilla install through the distri's package manager.

## Requirements

No special requirements.

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
          <li>boundary</li>
          <li>consul</li>
          <li>nomad</li>
          <li>packer</li>
          <li>terraform</li>
          <li>vagrant</li>
          <li>vault</li>
          <li>waypoint</li>
        </ul>
      </td>
      <td>Allows for a subselection of products to be installed. Defaults to the whole suite.</td>
    </td>
  </tbody>
</table>

## Dependencies

No dependencies.

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
      - boundary
      - consul
      - nomad
      - packer
      - terraform
      - vagrant
      - vault
      - waypoint

  roles:
    - role: chrisvanmeer.hashicorp
```

## License

MIT
