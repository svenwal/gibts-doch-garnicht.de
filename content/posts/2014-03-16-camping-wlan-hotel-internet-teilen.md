---
author: sven
categories:
- Debian
- Raspberry Pi
date: "2014-03-16T21:13:28Z"
guid: http://www.gibts-doch-garnicht.de/?p=118
id: 118
title: Camping- / WLAN- / Hotel-Internet teilen
url: /camping-wlan-hotel-internet-teilen/
---

Das hier wird ein noch wachsender Eintrag rund um mein Setup, welches ich nutzen werde, um z.B. auf Campingplätzen deren WLAN auf alle unsere Geräte zu verteilen ohne dass diese neu konfiguriert werden sollen.

Im Wohnwagen soll es konstant immer ein WLAN geben („MEIN\_WLAN“), welches von allen Clients verwendet wird. Für den Aufbau verwende ich einen Raspberry Pi (mit Raspian bzw. Raspbmc), eine kleine WLAN-Karte, ein simples CAT 5 Kabel und eine ausgemusterte Speedport 500V (welche ich im Keller gefunden habe).

Schritt 1: Raspberry Pi Grundinstallation (WLAN noch nicht gesteckt – Internet per LAN-Kabel)

Installation geht wirklich leicht von der Hand – [System herunterladen und den Anweisungen dort folgen](http://www.raspbmc.com/download/)

Schritt 2: Wichtige Anpassungen

Ziemlich genervt musste ich erstmal mit der englischen Tastaturbelegung in der Konsole kämpfen – diese stellt man wie [auf dieser Seite](http://sparky0815.de/2012/06/raspberry-pi-erste-schritte-debian/) beschrieben erstmal auf deutsch um – dann klappt es auch mit z,y,-,…

Schritt 3: Raspberry Pi wird Access Point

Im Gegensatz zum häufigeren Fall wollen wir, dass unser Raspberry Pi ein eigenes WLAN (eben das „MEIN\_WLAN“) aufmacht – dazu folge man einfach [dieser Anleitung](http://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point/install-software). Wenn alles klappt, müsste danach auf Euren Rechnern ein „MEIN\_WLAN“ als Verbindung verfügbar sein – und wenn der Raspberry Pi noch am WLAN hängt (was er sollte), dann kann man über das selbst erstellte WLAN schon surfen.

Schritt 4: (optional) Einen eigenen Nameserver aufsetzen

Ich will in meinem internen Netz alle Rechner immer unter einem Namen ansprechen – daher habe ich [gemäß dieser Anleitung PowerDNS installiert](http://www.ducky-pond.com/posts/2013/Oct/how-to-setup-a-dns-server-with-powerdns-on-raspberry-pi/) (bisher hatte ich immer Bind im Einsatz – aber das große Monster wollte ich dann doch nicht auf dem kleinen Pi haben).

Schritt 5: Schluss mit dem vorhandenen LAN

Der Raspberry Pi ist soweit eigentlich fertig – nun verheb ich auf der LAN-Schnittstelle via /etc/network/interfaces eine feste IP-Adresse in einem anderen Netzwerk als jenes des WLAN (sagen wir WLAN hat 192.168.1.xxx, so setze ich eth0 auf 192.168.2.1

Dann stelle ich noch ein, dass alle Verbindungen, welche nicht im WLAN laufen sollen, über eth0 und dort über die Adresse 192.168.2.2 gehen sollen (nein, Ihr habt nichts verpasst – das ist eine noch nicht belegte…)

> route add 192.168.2.0 eth0  
> route add default gw 192.168.2.2

Schritt 6: Die Speedport 500V wird zum Bitswitcher

Wir wollen, dass unser WLAN-Router nicht mehr ein WLAN aufspannt, sondern als Client an einem solchen teilnimmt. Das geht wohl ganz gut mit DD-WRT (dafür hatte ich die Hardware nicht da), auch Fritz!Boxen kriegt man wohl leicht dazu – ich aber hatte wie gesagt im Keller „nur“ die olle Speedport 500V gefunden.

Deren Telekom-Firmware kann den Client-Mode (natürlich) nicht, es gibt aber eine alternative Firmware namens „[Bitswitcher](http://bitswitcher.sourceforge.net/)“ – und die habe ich darauf installiert.

Schritt 7: Das LAN der Speedport umstellen

Wenn man sich über das Default-WLAN von Bitswitcher dort anmeldet, kann man dort das LAN umstellen – wir nehmen dort eine feste IP (192.186.2.2 – ja, die von vorhin) und wenn wir alles richtig gemacht haben (manchmal mag Bitswitcher einen Reboot), dann sollten wir vom Raspberry Pi (den wir ja im WLAN „MEIN\_WLAN“ erreichen können) bei gestecktem Kabel von LAN zu LAN ein ping gehen.

Schritt 8: Speedport mit einem fremden WLAN verbinden

Das Verbinden mit einem fremden WLAN benötigt insgesamt drei Einstellungen – auch hier hilft manchmal neben dem „Save &amp; Run“ ein beherzter Neustart via Aus-Schalter weiter):

1. Unter „Wireless LAN“ -&gt; „Basic Settings“ tragen wir als Mode „Client“ ein – und die Daten des zu verbundenen WLANs (Name, Kanal) und stellen auf „separate“ und schalten das DHCP dort an
2. Unter „Wireless LAN“ -&gt; „Security Settings“ tragen wir die Art der Verschlüsselung und das Passwort ein
3. Und das ist wichtig – muss aber nur einmal gemacht werden: Unter „Firewall“ schalten wir im Bereich „General Settings“ das WAN Interface auf „WLAN“ (damit dort die Weiterleitung auch klappt.

Erste Zusammenfassung: mit dem Setup schalte ich nun beide Geräte ein, rufe die IP-Adresse meines Speedport auf (bzw. habe ich im DNS einen entsprechenden DNS hinterlegt) und trage wie in Punkt 8 beschrieben die Daten des WLAN des Hotels, Campingplatzes usw. ein und alle Geräte sind glücklich.

Dieser Eintrag wurde in solch einer Konfiguration geschrieben 🙂

**UPDATE:** Auch wenn all das da oben funktioniert wie beschrieben – mittlerweile nutze ich einen [TP-Link TL-MR-3040](http://www.amazon.de/gp/product/B007W7UJTQ?ie=UTF8&camp=1638&creativeASIN=B007W7UJTQ&linkCode=xm2&tag=hundewissende0c) – dieser bietet mit der aktuellsten Firma im sogenannten WISP-Modus faktisch all das Out of the Box 🙂