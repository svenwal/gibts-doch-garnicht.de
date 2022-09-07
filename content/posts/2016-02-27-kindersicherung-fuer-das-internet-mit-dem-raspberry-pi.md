---
author: sven
categories:
- Blog
- Dansguardian
- Debian
- Netzwerk
- Raspberry Pi
date: "2016-02-27T11:49:41Z"
guid: http://www.gibts-doch-garnicht.de/?p=281
id: 281
title: Kindersicherung für das Internet mit dem Raspberry Pi
url: /kindersicherung-fuer-das-internet-mit-dem-raspberry-pi/
---

Jeder, der Kinder hat, sollte sich ab einem bestimmten Alter ernsthaft Gedanken machen, wie man diese vor den negativen Seiten des Internets so gut wie möglich schützen kann, ohne gleich das moderne Teufelszeug komplett zu verbieten. Dazu aber vorab: es muss einem klar sein, dass man es am Ende nur erschweren kann. Jedes halbwegs pfiffige Kind findet Wege, um auf das Netz zuzugreifen – und sei es nur, in dem es einfach zu einem/r Freund(in) geht, wo das WLAN offen ist.

Ich habe hier nun ein Kombination von FritzBox und Dansguardian auf dem Raspberry Pi im Einsatz. Die FritzBox macht zwei Dinge: 1. die Geräte der Tochter generell vom Internet ausschließen (Mail ausgenommen) und b) auch den verwendeten Raspberry Pi zeitlich beschränken – ab 20:15 geht das Internet dort aus.

Hauptkomponente für die Kindersicherung ist ein [Raspberry Pi](https://www.raspberrypi.org), auf welchem [Dansguardian](http://dansguardian.org) installiert ist. Praktischerweise ist Dansguardian Bestandteil von Raspbian, daher ist für die Installation nicht mehr nötig als

sudo apt-get install dansguardian squid

Dies installiert sowohl Dansguardian als auch den Proxy Squid auf dem System. Dann folgte ich letztlich der Anleitung unter [http://dokuwiki.nausch.org/doku.php/centos:dansguardian\_2.10](http://dokuwiki.nausch.org/doku.php/centos:dansguardian_2.10) – das werde ich jetzt hier nicht nochmal nachbeten, aber man sieht schon, dass die Installation unter [Raspbian](https://www.raspbian.org) einfacher ist als unter dem im Link verwendeten [CentOS](https://www.centos.org) 🙂

Statt also das volle Setup zu beschreiben (vielleicht mag das „jemand“ machen, der dies hier liest und dessen Raspberry Pi diese Funktionen eben noch nicht fertig installiert hat…) möchte ich nur die wichtigsten Eckpunkte hier zusammenfassen, die ich hintergelegt habe.

1. Wie oben schon gesagt verbietet meine FritzBox den Geräten meiner Tochter den Internetzugriff generell (damit ist diese Möglichkeit des Aushebelns versperrt)
2. Auch nutze ich die FritzBox für die zeitliche Kontrolle. Das geht grundsätzlich auch in Dansguardian, aber realistisch ist es so, dass man mal flexibel die Online-Zeit ändern möchte (Hausaufgaben-Recherche am Wochenende dauert länger…) und das geht im User-Interface der FritzBox nun mal am einfachsten
3. Der Raspberry Pi ist kein Router, also auch wenn man diesen als Gateway im Client hinterlegt, kommt man damit nicht ins Internet
4. DNS-Eintrag und/oder IP-Adresse des Raspberry Pi sollten fix sein, damit man ihn als Proxy hinterlegen kann
5. Der installierte Squid sollte nur auf localhost lauschen (sonst wird das informierte Kind dessen Port herausfinden und ihn direkt nutzen)
6. Gerade in der Anfangsphase am besten mal mit dem Kind und dessen iPad, iPhone, Rechner, … es alles machen lassen, was es machen möchte und dabei einen scharfen Blick auf die Logs haben. Dabei finden sich dann irgendwelche Online-Dienste (insb. Spiele, welche Daten in die Wolke schicken), welche geblockt werden. Die kann man dann in die Ausnahmen von Dansguardian aufnehmen

Zum Abschluss möchte ich noch einmal betonen: wo ein Wille ist, da wird das Kind einen Weg finden. Ich selber weiß mehrere verschiedene Wege, wie man solche Systeme umgehen kann (sage sie hier aber nicht :)). Daher prüfe ich regelmäßig mal nach, ob die Logfiles von Dansguardian zu den Zugriffen passen – wenn da offensichtlich Einträge fehlen, dann wird der genommene Weg gefunden und abgewürgt.

Natürlich könnte ich es nahezu 99% sicher hinbekommen (nur Whitelisting erlauben) – aber a) ist das dann sch\*\*\* zu pflegen, b) geht dann immer am Ende irgendwas nicht und c) bleibt immer noch das eine Prozent über (ich werde jetzt hier nicht zu viel dazu sagen, aus welchen beschnittenen Firmennetzen ich bisher trotzdem immer am Ende mit Vollzugriff rausgekommen bin…).