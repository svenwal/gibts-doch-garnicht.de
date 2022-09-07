---
author: sven
categories:
- Aufreger
- Netzwerk
date: "2015-09-25T21:00:47Z"
guid: http://www.gibts-doch-garnicht.de/?p=176
id: 176
title: Ausschalter
url: /ausschalter/
---

Heute wollte ich mal wieder einen Podcast aufnehmen und direkt vor Aufnahmebeginn brach mein Netzwerk zusammen. Alle Geräte meckerten auf einmal, dass die IP-Adressen schon belegt wären, holten sich neue und die war dann wieder belegt. Panik kroch in mir hoch und die Aufnahme fiel direkt ins Wasser.

Hilft ja nichts, Fehlersuche musste eingeleitet werden. Alle Komponenten mal durchbooten (FritzBox, 2\* Raspberry Pi, 2\* AirPort Extreme, 2\* WLAN2LAN Bridge usw.). Keine Besserung. Notebook direkt am LAN-Port der FritzBox: keine Besserung – bis dort alle anderen Geräte bis auf einen Raspberry Pi (mein DHCP und DNS Server) abgesteckt waren -&gt; Netz geht.

Damit kann man arbeiten: Langsam einzeln Geräte wieder zuschalten und am Ende (das dauerte eine ganze Weile bis der Schuldige gefunden war). Auf meinem Schreibtisch steht u. a. ein Cisco 7960 als VoIP-Telefon. Dessen Stromstrecker hatte ich gezogen, damit bei der Aufnahme keiner stören kann. Erkenntnis: wenn der Strom aus ist, das LAN-Kabel aber noch steckt, dann krallt sich das Telefon alle IP-Adressen.

Also ein toller Ausschalter für das gesamte Netz ist: Stecker am Telefon ziehen und ein paar Sekunden warten.

Da muss man erstmal drauf kommen…