# Podman Ansible role

An Ansible role for installing and configuring Podman to run rootful and
rootless containers in Rocky Linux 9, though likely supporting older versions
and other OSes.

## Usage

To configure a user for rootless Podman support, specify the user as variable
`podman_user` when invoking the role.

By default, this replaces the default registry list with the sole entry of
`["docker.io"]`.  If you want to use a different set of registries by default,
use the `podman_registries` variable.

Finally, this assumes you want all Podman users to be in a single group to
manage access to Podman system resources.  This group is set by the variable
`podman_group`, which defaults to `podman`.

```yaml
- name: Podman configuration
  hosts: all
  vars:
    podman_user: podman
    podman_registries: "[\"docker.io\", \"quay.io\"]"  # optional
    podman_group: podman  # optional
  roles:
    - podman-ansible-role
```

## License

MIT

## Author Information

Randy Eckman (Stretch Your Mind Entertainment LLC)
