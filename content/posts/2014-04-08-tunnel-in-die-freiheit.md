---
author: sven
categories:
- Debian
date: "2014-04-08T21:59:52Z"
guid: http://www.gibts-doch-garnicht.de/?p=121
id: 121
title: Tunnel in die Freiheit
url: /tunnel-in-die-freiheit/
---

Ausgehend vom [letzten Eintrag für meine Hotel/Camping-WLAN-Konfiguration](https://www.gibts-doch-garnicht.de/camping-wlan-hotel-internet-teilen/ "Camping- / WLAN- / Hotel-Internet teilen") kam auch eine Frage zum Thema „wie tunnele ich meine Netzverkehr durch die Firewall?“. Und da verwende ich seit Jahren ein schon so ziemlich überall erfolgreich verwendetes Setup, welches ich nun mal beschreiben möchte.

**Vorab**: Etwas technisch Know-how sollte vorhanden sein, denn die verwendeten Technologien sind nicht wirklich immer einfaches Plug&amp;Play.

Die **Grundidee** ist wie folgt: Auf einem Server (Rootserver oder vServer) installieren wir SSH und einen Proxy und schicken den Datenverkehr durch den SSH-Zugang zum Proxy, der es dann weiter ins Internet schickt. Der Gag dabei: SSH läuft nicht (bzw. nicht nur) auf Port 22, sondern auf Port 443, welcher normalerweise für HTTPS verwendet wird und daher von Firewalls nahezu immer erreichbar ist.

**Benötigte Software**: Wir benötigen einer Rootserver (auch als vServer klappt das) mit einem Linux als Betriebssystem (ich verwende Debian – selbstverständlich gingen auch \*\*\*BSD und ähnlich), auf welchem SSH und der Proxy-Server Squid installiert werden. Auf dem Client (also dem Rechner, von welchem wir surfen wollen) entweder einen SSH-Client oder aber Putty (was unter Windows meist die Regel sein dürfte).

**Setup von SSH**: ich gehe mal davon aus, dass der Server, welchen Ihr mietet, eh schon per SSH erreichbar ist. Das ergänzen wir nun um den Port 443, indem wir in /etc/ssh/sshd\_config die Einträge für die Ports, damit dann 22 und 443 verwendet werden:

Port 443  
Port 22

Nach einem Neustart von SSH sollte dieses nun auch über den Port 443 erreichbar sein (parallel darf dann natürlich nicht z.B. ein Webserver diesen Port nutzen wollen).

**Proxy-Server:** Als Proxy verwende ich (mehr oder weniger aus Gewohnheit) Squid. Erstmal fast im Standard installiert, allerdings mit diesem einen speziellen Eintrag:

http\_port 127.0.0.1:3128

Soll heißen: ich will nicht, dass irgendwer von außerhalb meine Proxy missbraucht, daher lasse ich ihn nur auf der internen Netzwerkadresse laufen (127.0.0.1 ist das Loopback-Device)

**Der Tunnel**: Eine tolle Funkionen von SSH: Man kann beliebige Adressen/Ports hindurchschleifen. In diesem Beispiel machen wird folgendes: Wir melden uns vom Client mittels SSH am Server an und dabei wird der Port 3128 (der Proxy) auf dem Client als Port 13128 zur Verfügung gestellt. Das heißt dann, dass man im Webbrowser als Proxy den Server 127.0.0.1 (also lokal) mit dem Port 13128 einstellt und schon ist man über dem Weg draußen.

ssh meinNutzer@meinServer.de -p 443 -L 13128:127.0.0.1:3128

**Allgemeine Hinweise**: Ein eigener Server im Internet ist ein beliebte Angriffsquelle für Hacker, daher würde ich immer SSH so einstellen, dass es nur mit Public/Private-Key läuft und nicht per Passwort. Und außerdem sollte man den Rechner immer auf dem aktuellsten Stand haben und eine Idee haben, was das Linux eigentlich so tut.

**Nette Ergänzungen:** Im Squid kann man z. B. mittels „acl Safe\_ports port 12345“ diesen für weitere Ports verwenden und so z. B. Chat-Clients über diesen laufen lassen.

Und man kann im SSH-Aufruf auch mehrere Weiterleitungen einstellen und so z. B. mittels

ssh meinNutzer@meinServer.de -p 443 -L 13128:127.0.0.1:3128 -L 13993:imap.gmail.com:993

den Zugriff auf seine Gmail-Mails auch durch die Firewall machen (und z. B. im Thuderbird dann als IMAP-Server 127.0.0.1 auf dem Port 13993 einstellen

**Eins noch**: Ich habe absichtlich keine Schritt-für-Schritt-Anleitungen für z. B. die Installation von Squid hier mit aufgeführt – wenn Ihr das nicht hinbekommt (ggf. mit Hilfe von Goolge), dann rate ich Euch dringend davon ab, einen eigenen Server zu betreiben…