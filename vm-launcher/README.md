# vm - Simple VM Launcher and Manager

🇧🇷 [Versão em Português](README.pt-br.md)

A lightweight bash wrapper around libvirt/virsh for quickly launching, connecting, editing, and stopping QEMU/KVM virtual machines.

## Installation

```bash
sudo cp vm /usr/local/bin/vm
sudo chmod +x /usr/local/bin/vm
```

## Commands

| Command | Description |
|---------|-------------|
| `vm list` | List all VMs and their current state |
| `vm start <n>` | Start a VM and open virt-viewer |
| `vm stop <n>` | Graceful ACPI shutdown (60s timeout) |
| `vm stop <n> --force` | Force kill the VM immediately |
| `vm viewer <n>` | Reconnect virt-viewer to a running VM |
| `vm edit <n>` | Edit VM XML config (opens virsh edit) |
| `vm status <n>` | Show detailed VM info (vCPUs, RAM, state) |

## Usage Examples

```bash
# See what's available
vm list

# Start your Windows VM and connect
vm start win11-office

# Reconnect if you closed the viewer window
vm viewer win11-office

# Change VM settings (CPU, RAM, video, devices)
vm edit win11-office

# Done working — graceful shutdown
vm stop win11-office

# VM frozen? Force kill it
vm stop win11-office --force
```

## Requirements

- `libvirt` + `virsh`
- `virt-viewer`
- `sudo` access for virsh commands

## Notes

- `vm start` automatically opens virt-viewer in the background — you get your terminal back immediately
- `vm stop` sends an ACPI shutdown signal (like pressing the power button) and waits up to 60 seconds before timing out
- `--force` is equivalent to pulling the power cable — only use if the VM is unresponsive
- Closing the virt-viewer window does **not** stop the VM — use `vm stop` for that
- The `--wait` flag on virt-viewer means it will reconnect automatically if the VM reboots
- `vm edit` opens the VM XML in your default editor (`$EDITOR`). If the VM is running, changes apply after a full shutdown (not reboot)
