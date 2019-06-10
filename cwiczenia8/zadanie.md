Zadanie 1
---------

![zadanie 1](zadanie-1.svg)

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
---------
Rozwiązanie:
---------
Podział sieci 
-------------
| sieć | adres |
|:-----|:------|
| LAN1 | 172.22.160.0/23 |
| LAN2 | 172.22.128.0/19 |

PC0
---
|  interfejs   | adres  |
|:-------------| :------| 
| eth0 | zapewnia usługodawca |
| eth1 | 172.22.160.1/23  |
| eth2 | 172.22.128.1/19  |

PC1
---
|  interfejs   | adres  |
|:-------------| :------| 
| eth0 | 172.22.160.2/23 |

PC2
---
|  interfejs   | adres  |
|:-------------| :------| 
| eth0 | 172.22.128.2/19 |

--------------
Ustawienie adresów IP 
---
ip addr add (adres) dev (interfejs) 
Umożliwienie przekazywania adresów IP w PC0
---
tymczasowo:  echo 1 > /proc/sys/net/ipv4/ip_forward ,  na stałe: sysctl -w net.ipv4.ip_forward=1

Trasowanie - ustawienie trasy domyślnej dla PC1 i PC2 
---
Ustawienie trasy domyślnej prowadzącej przez PC0 instrukcją : ip route add default via (adres interfejsu podłączonego do danej sieci w PC0) 
Dodanie dns w PC1 i PC2 
---
wejście do pliku /etc/resolv.conf
i dodanie nameserver 8.8.8.8

Umożliwienie przekazywania internetu w PC0
---
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE


