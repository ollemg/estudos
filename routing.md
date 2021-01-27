# Routing and switching

## config de interface

/etc/sysconfig/network-scripts/ifcfg-eth0:

```bash
DEVICE=eth0
BOOTPROTO=static
ONBOOT=yes

IPADDR=10.10.10.10
NETMASK=255.255.255.0
GATEWAY=10.10.10.1
DNS1=10.10.10.2
DNS2=10.10.10.3
DNS3=10.10.10.4


TYPE=Ethernet
DEFROUTE=yes

IPV6_AUTOCONF=no
IPV6_DEFROUTE=no
```

## Multiplas interfaces e metricas

Configurar as metricas:

/etc/iproute2/rt_tables:

```bash
1 link1
2 link2
3 link3
```

adicionando a rota default:

ip route add default via 10.10.10.1 dev eth0 table link1

adicionando as outras rotas:

ip route add 10.10.10.0/24 dev eth0 src 10.10.10.10 table link1
ip route add 10.10.10.0/24 dev eth1 src 10.10.10.11 table link2
ip route add 10.10.10.0/24 dev eth2 src 10.10.10.12 table link3

