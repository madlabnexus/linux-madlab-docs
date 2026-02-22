# vm - Gerenciador Simples de VMs

🇺🇸 [English version](README.md)

Um wrapper bash leve para libvirt/virsh para iniciar, conectar, editar e parar rapidamente máquinas virtuais QEMU/KVM.

## Instalação

```bash
sudo cp vm /usr/local/bin/vm
sudo chmod +x /usr/local/bin/vm
```

## Comandos

| Comando | Descrição |
|---------|-----------|
| `vm list` | Listar todas as VMs e seus estados |
| `vm start <n>` | Iniciar VM e abrir virt-viewer |
| `vm stop <n>` | Desligamento gracioso via ACPI (timeout 60s) |
| `vm stop <n> --force` | Forçar encerramento imediato da VM |
| `vm viewer <n>` | Reconectar virt-viewer a uma VM em execução |
| `vm edit <n>` | Editar XML de configuração da VM (abre virsh edit) |
| `vm status <n>` | Mostrar detalhes da VM (vCPUs, RAM, estado) |

## Exemplos de Uso

```bash
# Ver o que está disponível
vm list

# Iniciar sua VM Windows e conectar
vm start win11-office

# Reconectar se fechou a janela do viewer
vm viewer win11-office

# Alterar configurações da VM (CPU, RAM, vídeo, dispositivos)
vm edit win11-office

# Terminou de trabalhar — desligamento gracioso
vm stop win11-office

# VM travou? Forçar encerramento
vm stop win11-office --force
```

## Requisitos

- `libvirt` + `virsh`
- `virt-viewer`
- Acesso `sudo` para comandos virsh

## Observações

- `vm start` abre o virt-viewer automaticamente em segundo plano — seu terminal fica livre imediatamente
- `vm stop` envia um sinal ACPI de desligamento (como pressionar o botão de energia) e aguarda até 60 segundos antes de expirar
- `--force` é equivalente a puxar o cabo de energia — use apenas se a VM não estiver respondendo
- Fechar a janela do virt-viewer **não** para a VM — use `vm stop` para isso
- O flag `--wait` no virt-viewer faz ele reconectar automaticamente se a VM reiniciar
- `vm edit` abre o XML da VM no seu editor padrão (`$EDITOR`). Se a VM estiver rodando, as alterações só valem após desligamento completo (não reboot)
