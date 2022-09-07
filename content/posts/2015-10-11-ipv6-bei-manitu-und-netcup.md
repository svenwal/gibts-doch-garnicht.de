---
author: sven
categories:
- Debian
- IPv6
date: "2015-10-11T11:45:02Z"
guid: http://www.gibts-doch-garnicht.de/?p=195
id: 195
title: IPv6 bei manitu und netcup
url: /ipv6-bei-manitu-und-netcup/
---

Ich fahre schon eine ganze Weile meinen Hauptserver bei [manitu](https://www.manitu.de/) und mein Backupserver ist aktuell bei [netcup](https://www.netcup.de/) (u. a. die Verfügbarkeit von [IPv6](https://de.wikipedia.org/wiki/IPv6) ließ mich damals wechseln). Also (fast) alle Dienste laufen auf manitu und die Konfiguration wird täglich als Sicherung zu meinem netcup-Server übertragen (welcher aber nebenher auch 2 oder 3 Dienste bereitstellt, welche aus diversen Gründen nicht bei manitu liegen – meist wollte ich den Hauptserver nicht zu sehr in die Schusslinie bringen).

Wie auch immer, bei beiden Anbietern könnt Ihr bequem im Kundeninterface IPv6 aktivieren und bekommt einen Adressblock mit Millionen von Adressen (und damit wäre auch schon einer der riesigen Vorteile von IPv6 genannt – jeder Dienst, jede Subdomain bekommt bei mir seither eine eigene IPv6 – bei IPv4 musste ich bis dato mit ingesamt fünf auskommen).

In der Aktiverung der Adressen unterscheiden sich die beiden aber etwas. Zum einen habe ich bei manitu noch Debian 7.x am laufen, zum anderen ist die Maschine bei netcup nur virtuell.

Bei manitu / Debian 7.x füge ich neue Adressen in /etc/network/interface so hinzu:  
```bash
# The primary network interface
auto eth0
iface eth0 inet static
address 89.238.64.35
netmask 255.255.255.0
network 89.238.64.0broadcast 89.238.64.255
gateway 89.238.64.1
# dns-* options are implemented by the resolvconf package, if installed
dns-nameservers 217.11.48.200 217.11.49.200
```

```bash
iface eth0 inet6 static
address 2a00:1828:2000:370::2
netmask 64
gateway 2a00:1828:2000:370::1
```

```bash
up /sbin/ifconfig eth0 inet6 add 2a00:1828:2000:370::3/64
```

```bash
up /sbin/ifconfig eth0 inet6 add 2a00:1828:2000:370::4/64
```

Oder kurzgefasst: die erste IPv6 gebe ich direkt per address an, alle weiteren mittels /sbin/ifconfig eth0 inet6 add 2a00:1828:2000:370::xxxx/64.

Als positiven Nebeneffekt kann man den entsprechenden ifconfig-Aufruf einfach in die Shell werfen und das Interface ist sofort da.

Bei netcup / Debian 8 sieht es etwas anders aus. Auch dort ist ein Eintrag in /etc/network/interfaces zu platzieren, welcher aber wie folgt aufgebaut ist:

```bash
# The primary network interface
auto eth0
iface eth0 inet static
address 37.120.175.72
netmask 255.255.252.0
broadcast 37.120.175.255gateway 37.120.172.1
```

```bash
iface eth0 inet6 stati
address 2a03:4000:6:70b3::1
netmask 64gateway fe80::1
```

```bash
auto eth0:1
iface eth0:1 inet6 static
address 2a03:4000:6:70b3::2<br></br>netmask 64
```

```bash
auto eth0:2
iface eth0:2 inet6 static
address 2a03:4000:6:70b3::3
netmask 64
```

Hier werden also alle Adressen mittels eines neues eth0:x-Eintrages hinzugefügt. Es gibt zwei böse Fallen, welche einen bei einem netcup-vServer erwarten:

1. Die Änderung wird erst aktiv, wenn man den virtuellen Server **ausschaltet**. Und damit meine ich im Kundeninterface den Power-Off, nicht ein „reboot“ oder ähnlich in der Shell.
2. Wenn man die IPv6-Adressen hinzufügt, dann sind diese ja statisch (wie man auch sieht). Dabei muss man aber auf jeden Fall **auch jene vom IPv4 statisch setzen**. Lässt man diese auf DHCP (was der Default ist), so läuft es einige Minuten (ca. eine halbe Stunde im Schnitt) wie es soll. Dann holt sich die IPv4 per DHCP ein Update und überschreibt in dem Schritt die Default-Route des IPv6 mit. Die Adressen sind dann noch da, mangels korrektem Routing sind sie aber nicht erreichbar. Durch die Verzögerung eine böse Falle.