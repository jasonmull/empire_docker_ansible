# Empire C2 Docker

Deploy [Empire C2](https://github.com/BC-SECURITY/Empire) via Docker. Perfect for red team labs and [Ludus](https://ludus.cloud/) ranges.

## Install

**Ansible Galaxy:**
```bash
ansible-galaxy install jasonmull.empire_c2_docker
```

**Ludus:**
```bash
# On your Ludus host
ludus ansible roles add jasonmull.empire_c2_docker
ludus ansible roles list  # verify installation
```

## Usage

**Basic:**
```yaml
- hosts: target
  roles: [jasonmull.empire_c2_docker]
```

**Ludus:**
```yaml
ludus:
  - vm_name: "{{ range_id }}-empire-c2"
    hostname: "empire-c2"
    template: debian-12-x64-server-template
    vlan: 10
    ip_last_octet: 10
    ram_gb: 4
    cpus: 2
    linux: true
    testing:
      snapshot: false
      roles:
        - jasonmull.empire_c2_docker
      vars:
        empire_container_name: "{{ range_id }}-empire"
        empire_data_volume: "{{ range_id }}-empire-data"
```

## Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `empire_image` | `bcsecurity/empire:latest` | Docker image |
| `empire_container_name` | `empire` | Container name |
| `empire_data_volume` | `empire-data` | Volume name |

## Access

```bash
docker exec -it empire /bin/bash
```

## Requirements

- Debian/Ubuntu + Docker
- `ansible-galaxy collection install community.docker`

⚠️ **Authorized testing only**

## License

MIT
