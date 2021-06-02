# Tópico 102: Instalação do linux e gerenciamento de pacotes

- 102.1 Design do Layout do HD (2)
- 102.2 Instalação do boot manager (2)
- 102.3 Gerenciamento de Bibliotecas Compartilhadas (1)
- 102.4 Gerenciamento de Pacotes Debian (3)
- 102.5 Gerenciamento de Pacotes RPM e YUM (3)
- 102.6 Linux e Virtualização (1)

---
## 102.1

### Partição e ponto de montagem

Partição: sda1,sda2
Ponto de montagem: /home, /var

Minimo ter 2 partições

Vangatens de particionar o disco:

- Controle de espaço em disco
- Mais de um sistema de arquivos para diferentes aplicações
- Proteção contra erros de disco
- Diferentes niveis de segurança
- backup facilitado

### Sistemas de Particionamento

MBR: Master boot Record

- limitado a 2TB

GPT: GUID Partition Table

- Não limita em 2TB
- EFI

## MBR

Tipos de Partição:

- Primaria
- Extendida (Tipo de Primária): Contém as Partições Lógicas
- Lógica

Limitada a 4 partições primárias ou 3 primárias mais 1 extendida
Primárias numeradas de 1 a 4. ex: sda1,sda2,sda3,sda4
Lógicas numeradas a partir de 5. Ex: sda5, sda6, sda7

Partição / é a primeira a ser montada pelo kernel

Código dos tipos de Partição

- 0x83 = Linux FileSystem
- 0x82 = Linux swap

Partições comuns:

- /home (arquivos de usuários)
- /var (Arquivos de log, fila)
- /tmp (arquivos temporários)
- /boot (GRUB)
- /urs (Muitas aplicações)

Diretórios que não podem ser montados fora do /

- /etc (/etc/fstab)
- /bin (ficam os comandos)
- /sbin (ficam os comandos)
- /dev
- /proc
- /sys

### LVM

Logical Volume Management

Método para alocar espaço dos discos em volumes lógicos

Facilita o redimensionamento

Elementos:

- VG: volume Group
- PV: Phisical Volume
- LV: Logical Volume
- PE: Physical Extent
- LE: Logical Extent

### EFI, UEFI, ESP

comando para administrar o efi:

```bash
efibootmgr
```

Mais detalhado:

```bash
efibootmgr -v 
```
---
## 102.2

### GRUB

GRAND UNIFIED BOOT LOADER

#### GRUB LEGACY

arquvivo de configuração:

```bash
/boot/grub/menu.lst
```

```bash
/boot/grub/grub.conf/cfg
```

Referência de disco

No GRUB Legacy as referências dos discos começam em 0. Primeiro numero é referente ao disco e o segundo qual partição.

- hda1 = hd0,0
- hda5 = hd0,4
- hdb3 = hd1,2

Instala o bootloader na MBR

```bash
grub-install /dev/sda
```

```bash
grub-install '(hd0)'
```

#### GRUB2

arquvivo de configuração:

Sistema:

```bash
/boot/grub/grub.cfg
```

Administrador:

```bash
cat /etc/default/grub
```

```bash
/etc/grub.d/
```

Referẽncias de disco

Contagem do disco começa no 0
Contagem da partição começa pelo 1

- hda1 = hd0,1 ou hd0, msdos1
- hda5 = hd0,5
- hdb3 = hd1,3

Comandos:

```bash
grub-install <device>
```

Gera o grub.cfg:

```bash
update-grub
```

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```
---
### 102.3 Gerenciamento de Bibliotecas compartilhadas

Diretório padrão das bibliotecas:

```
ls /lib
```

```
ls /usr/lib
```

Mostra o compartilhamento de bibliotecas requeridos pelo programa:

```
ldd /bin/bash
```

Mostra as bibliotecas de um processo
```
pldd $$
```

Utilizado Para recompilhar o /etc/ld.so.cache:

```
ldconfig
```

Lista todas as bibliotecas que estão no ld.so.cache
```
ldconfig -p
```

Para incluir novos diretorios de lib, editar o arquivo /etc/ld.so.conf:

```
$ cat /etc/ld.so.conf                                                                                                                   [20:32:04]
include ld.so.conf.d/*.conf

```
Para importar novos diretorios de bibliotecas temporariamente, utilizar a variavel de ambiente LD_LIBRARY_PATH:

```
export LD_LIBRARY_PATH=/tmp/lib
```

---
# 102.4 Gerenciamento de Pacotes

|                                      | Padrão Debian                                                   | Padrão RPM/RedHat           |
| ------------------------------------ | --------------------------------------------------------------- | --------------------------- |
| Extensão                             | .deb                                                            | .rpm                        |
| Gerenciador de pacotes               | `dpkg`                                                          | `rpm`                       |
| Gerenciador de Pacotes + Repositório | `apt`                                                           | `yum`  `dnf`                |
| OUtros Comandos                      | `dpkg-reconfigure`  `apt-cache`  `dselect`  `aptitude`  `alien` | `yumdownloader`  `rpm2cpio` |
|                                      |                                                                 |                             |


Cada sistema deve usar um sistema de gerenciamento único

