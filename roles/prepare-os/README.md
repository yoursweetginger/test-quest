# Prepare OS

Ansible role prepare the server for operation:

- Encrypt the second disk in the system (where there is no root partition) (partition name should be specified in the inventory).
- Encrypt the partition that is present on the disk next to the root partition. The role will try to find a not mounted partition. If the partition is less than 16 MiB, the play will fail.
- Disable C-state for all available CPUs.
- Switch CPU operation from power-saving mode to more productive mode. If CPU is not supporting scaling governor, the play will skip.
- Rename the active network interface to "net0".
- List CPUs information.

## Preparation

1. Install requirements:

```bash
ansible-galaxy install -r requirements.yml -f
```

2. Set vars:

```yaml
# Name of the disk to encrypt
# Target disk should not be the root disk
encrypt_disk: xvdf
```

3. Create LUKS keyfile which will be used to encrypt the disk:

```bash
openssl genrsa -out keyfile 2048
```
