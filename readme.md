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

## SSH Keys

This role performs tasks that call `podman`, which, if done with a sudo user,
can cause Podman system misconfiguration for rootless containers running as
that user.  It is recommended to only perform tasks that call `podman` directly
as the user who will run the rootless container by using the `remote_user`
keyword.  This requires a new SSH connection as the given user, but will attempt
to use the default private key of the current Ansible invocation.  Therefore,
it is important to ensure that the ansible user's public key is also in the
`authorized_keys` file for the Podman user that will run the container.

## License

MIT

## Author Information

Randy Eckman (Stretch Your Mind Entertainment LLC)
