# Tópico 101

## 101.1

### BIOS

- BIOS: Basic Input Output System
- POST: Power-On Self-Test
- Gerencia de Dispositivos, IRQ, I/O, DMA
- Inicia o Processo de Boot
- EFI Extensible Firmware Interface
- UEFI Unified EFI

### IRQ (Interrupt Request)

- Sinal enviado ao CPU
- Não deve haver conflitos

```bash
cat /proc/interrupts
```

Principais IRQs:

- IRQ1  - Teclado
- IRQ3  - Porta Serial 1
- IRQ4  - Porta Serial 2
- IQR9  - Placa de Vídeo
- IQR11 - Controlador USB
- IRQ14 - IDE Primária
- IRQ14 - IDE Secundária

### Endereços I/O (E/S)

Lista de endereços de memória utilizadas para comunicação ente a CPU e os demais dispositivos de hardware

```bash
cat /proc/ioports
```

### DMA (Direct Memory Addressing)

Um canal que permite que os dispositivos transmitam os dados diretamente para a meméria, sem utilizar a CPU. Não é utilizado por todos os dispositivos

```bash
cat /proc/dma
```

### Barramentos

- PCI: peripheral component interconnect

Ver os dispositivos:

```bash
lspci
```

Visualizar detalhadamente um barramento pci:

```bash
lspci -s 00:00.0 -v
```

- USB: Universal Serial Bus

Visualizar os dispositivos conectados

```bash
lsusb
```

Visualizar detalhadamente um barramento usb

```bash
lsusb -s 001:001 -v
```

## Partições Virtuais

- /proc: informações dos processos ativos e recursos de hardware
- /sys : informações sobre dispositivos de hardware (sysfs)
- /dev : Referências aos dispositivos do sistema, inclusive de armazenamento (udev)
- dbus : comunicação entre os processos
- ColdPlug X HotPlug

Argumentos que o bootloader passou pro kernel quando o sistema estava iniciando

```bash
cat /proc/cmdline
```

Tipos de Filesystem que podem ser utilizados

```bash
cat /proc/filesystems
```

O comando mount pega as informações desse arquivo:

```bash
cat /proc/mount
```

## Udev

Regras do Udev

```bash
cat /lib/udev/rules.d/
```

Para criar as proprias regras, ou outras aplicações

As regras são numeradas para ser executadas em ordem crescente

