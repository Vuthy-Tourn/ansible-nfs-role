# Ansible NFS Role as GitSubmodule

An Ansible role for installing, configuring, and managing NFS (Network File System) servers and clients.

## Features

- **NFS Server Configuration**: Set up and manage NFS exports
- **NFS Client Support**: Mount NFS shares on client systems

## Role Variables

### Server Variables

```yaml
nfs_server_enabled: true
nfs_version: 4
nfs_exports:
  - path: /srv/nfs_share
    clients:
      - host: "192.168.1.0/24"
        options: "rw,sync,no_subtree_check"
```

### Client Variables

```yaml
nfs_client_enabled: true
nfs_mounts:
  - src: "nfs-server.example.com:/srv/nfs/share1"
    path: /mnt/nfs_share
    opts: "defaults,_netdev"
    state: mounted
```

## Example Playbook

```yaml
---
- hosts: nfs_servers
  become: true
  roles:
    - role: ansible-nfs-role
      vars:
        nfs_server_enabled: true
        nfs_exports:
          - path: /srv/nfs/shared
            clients:
              - host: "192.168.1.0/24"
                options: "rw,sync,no_subtree_check"
```

## Directory Structure

```
ansible-nfs-role/
├── meta/
│   └── main.yaml
├── tasks/
│   ├── main.yaml
│   ├── setup-nfs-client.yaml
│   └── setup-nfs-server.yaml
└── README.md
```

## Usage as Submodule

Add this role as a submodule to your main Ansible project:

```bash
git submodule add https://github.com/Vuthy-Tourn/ansible-nfs-role roles/ansible-nfs-role
git commit -m "Add NFS role as submodule"
```

Reference in your playbook:

```yaml
roles:
  - ansible-nfs-role
```
