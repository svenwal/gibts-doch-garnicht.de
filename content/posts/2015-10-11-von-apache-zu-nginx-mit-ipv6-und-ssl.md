---
author: sven
categories:
- Debian
- IPv6
- Netzwerk
- nginx
- SSL
date: "2015-10-11T11:05:01Z"
guid: http://www.gibts-doch-garnicht.de/?p=187
id: 187
title: Von Apache zu nginx mit IPv6 und SSL
url: /von-apache-zu-nginx-mit-ipv6-und-ssl/
---

Seit ewigen Zeiten (irgendwas größer 15 Jahre) laufen alle meine Webseiten auf [Apache](https://httpd.apache.org/). Zu seiner Zeit war Apache die einzige wirkliche Wahl und die Gewohnheit siegt. Mit [Debian 8](https://www.debian.org/) steht nun für mich ein Update auf der ToDo-Liste, welches einige Änderungen an der Konfiguration nach sich ziehen würde (es ist eine lang gewachsene Konfiguration) und so fand ich, es wäre mal wieder Zeit etwas neues zu lernen.

Daher startete ich ein Migrationsprojekt mit folgenden Zielen:

- Alle Webseiten ziehen um auf [nginx](http://nginx.org/)
- Alle Webseiten werden über [IPv6](https://de.wikipedia.org/wiki/IPv6) erreichbar (bisher rund 2/3)
- Alle Webseiten werden nur noch mittels [HTTPS](https://de.wikipedia.org/wiki/Hypertext_Transfer_Protocol_Secure) ausgeliefert (HTTP-Anfragen werden automatisch weitergeleitet)

Wie immer war und ist Google ein guter Freund bei vielen Fragen (meine alte Konfiguration strotzt nur so von Alias, Redirect, RedirectMatch usw.) und ich will in einer Serie von Einträgen meine Erfahrungen und Konfigurationen hier veröffentlichen, damit sowohl ich als auch andere Leser nachvollziehen können, wie man das angehen kann.

Folgende Einträge führen zum Ziel (werden Stück für Stück geschrieben werden):

- [Einrichtung von IPv6 auf manitu und netcup-Servern](/ipv6-bei-manitu-und-netcup/)
- Installation und Grundkonfiguration nginx (folgt)
- Zertifikatserstellung mit [StartSSL](http://www.startssl.com/) (folgt)
- nginx und SSL ([Optimierung für moderne Protokolle](https://www.ssllabs.com/ssltest/analyze.html?d=gibts-doch-garnicht.de&latest)) (folgt)
- nginx und PHP (folgt)
- nginx und ein Host mit IPv6/IPv4 und SSL (http wird weitergeleitet) (folgt)
- nginx, locations und PHP (folgt)
- Herausforderungen mit [WordPress (folgt)](https://de.wordpress.org/)

Das wird ein paar Tage dauern, bis alle Einträge da sein werden – parallel werden nämlich noch einige weitere Domains umziehen.

Übrigens war und ist dieses Blog eines der ersten gewesen, welches ich ungezogen habe. Wenn Ihr das also lest, so habt Ihr es bereits mittels nginx beliefert bekommen und die Verbindung ist verschlüsselt.