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

### Partições Virtuais

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

### Udev

Regras do Udev

```bash
cat /lib/udev/rules.d/
```

Para os admins ou aplicações:

```bash
/etc/udev/rules.d
```

Para criar as proprias regras, ou outras aplicações

As regras são numeradas para ser executadas em ordem crescente

### Modulos

Local onde ficam os modulos do sistema

```bash
/lib/modules/$(uname -r)/
```

Local onde é possivel importar modulos

```bash
cat /etc/modules
```

### lsmod

visualiza os modulos carregados do sistema

```bash
lsmod
```

```bash
cat /proc/modules
```

### modinfo

comando para visualizar com detalhes um modulo

```bash
modinfo ip_tables
```

### rmmod

Remove um modulo carregado

```bash
rmmod nome_do_modulo
```

### insmod

carrega um modulo

```bash
insmod /lib/modules/3.10.0-1160.15.2.el7.x86_64/kernel/net/ipv4/netfilter/ip_tables.ko.xz
```

### modprobe

Gerenciador de modulos

Inserir modulos

```bash
modprobe nome_do_modulo
```

Remover Modulos

```bash
modprobe -r nome_do_modulo
```

Arquivos de configuração:

```bash
/lib/modprobe.d/
```

```bash
/etc/modprobe.d/
```

devtmpfs é o sistema de arquivos temporario que grava em memoria e não em disco

### Dispositivos de armazenamento

- IDE
  - /dev/hda ou sda - master
  - /dev/hdb ou sdb - slave
  - /dev/hdc ou sdc - master
  - /dev/hdd ou sdd - slave

- SCSI - Small Computer System Interface
  - tipo:
  - 8 bits (7 dispositivos 1 controlador)
  - 16 bits (15 dispositivos 1 controlador)
- SCSI_ID
  - canal - identificador de cada adaptador
  - ID - identificador de cada dispositivo
  - LUN - Número Lógico de Unidade
- Mapeamentos no Linux:
  - /dev/sda - Primeiro
  - /dev/sdb - Segundo
  - /dev/sdc - Terceiro
  - /dev/sdd - quarto
- /proc/scsi/scsi

### Processo de boot

Bios > MBR > Bootloader(GRUB/LILO) Kernel (Executa o /sbin/init) > Init (Inicia os programas do runlevel/target definido)

### MBR

Master Boot Record.

Localizado no primeiro setor do disco bootável

- /dev/hda ou /dev/sda

Contém informações sobre GRUB/LILO

MBR carrega e executa o GRUB/LILO

### Bootloader

Gerenciador de boot

Carrega o SO na mamória

GRUB = Grand Unified BootLoader

initrd/initramfs: também é carregado pelo bootloader para dar suporte ao kernel. filesystem root (/) temporário carregado em meméria RAM

### INIT

Tem a função de iniciar os processos e serviços no linux

É o processo de ID 1

Possui RunLevels ou Targets que definem diferentes modos de operação e o Grupo de Serviços que será iniciado

Principais INITs utilizados:

- SystemV (SysV)
- SystemD
- Upstart

### dmesg

log do boot da maquina e do funcionamento do sistema

```bash
dmesg | less
```

### PROCESSO DE BOOT - UEFI

UEFI >> bootloader >> Kernel >> init

ESP (EFI System Partition)

É montado no diretório /boot/efi

Utiliza um filesystem do tipo FAT

Utiliza GPT ao invés de MBR

Suporta partições além de 2TB

Boot Seguro (Imagem do kernel assinada)

Configurado pelo UEFI Boot Manager

```bash
efibootmgr
```

### journalcrl

Coleta de logs e informações de boot

Informações de boot:

```bash
journalctl -b
```

Informações do Kernel

```bash
journalctl -k
```

Informações em tempo real

```bash
journalctl -f
```

### Gerenciadores de Inialização

- SystemV
- SystemD
- Upstart

### SystemV

Runlevels

- 0 desligamento
- 1, s, S Single User
- 2 Multiuser (sem rede)
- 3 Multiuser (com rede)
- 4 Multiuser (definido pelo usuario)
- 5 Multiuser (com rede e gráfico)
- 6 reinicialização

Cada runlevel carrega um conjunto de programas, scripts e serviços
cfg princial

```bash
/etc/inittab
```

Diretório de scripts

```bash
/etc/init.d/
```

```bash
/etc/rc.d
```

### SystemD

Units
Grupo de Units (Targets)

Tipos de unidades:

- service
- socket
- device
- mount
- automount
- target - equivale ao runlevel
- snapchat

Diretório principal

```bash
/lib/systemd/system/
```

Mudar runlevel

```bash
systemctl set-default grafical.target
```

```bash
systemctl isolete rescue.target
```

### shutdown

Sem nenhum parametro será agendado para desligar em 1 minuto:

```bash
shutdown
```

Cancelar o shudown:

```bash
shutdown -c
```

Desligar o linux (não desliga a maquina)

```bash
shutdown -h
```

Agendar desligamentos

```bash
shutdown 18:00
```

```bash
shutdown +90
```

### Wall

Manda mensagem para os outros usuarios

```bash
wall "mensagem"
```

### APCI

Advanced Configuration and Power Interface
