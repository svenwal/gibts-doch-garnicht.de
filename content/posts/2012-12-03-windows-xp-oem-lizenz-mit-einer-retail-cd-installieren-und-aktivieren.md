---
author: sven
categories:
- Blog
- Windows
date: "2012-12-03T17:57:52Z"
guid: http://www.gibts-doch-garnicht.de/?p=68
id: 68
title: Windows XP OEM Lizenz mit einer Retail-CD installieren und aktivieren
url: /windows-xp-oem-lizenz-mit-einer-retail-cd-installieren-und-aktivieren/
---

Nach dem ganzen [Mist mit dem missglückten Upgrade meiner Windows XP-Maschine auf Windows 8](https://www.gibts-doch-garnicht.de/kleiner-ausflug-in-die-windows-holle/ "Kleiner Ausflug in die Windows-Hölle") musste der XP-Rechner wieder neu aufgesetzt werden (und wird nun Age of Empires-Spielrechner und Entwicklungs-Testsystem).

Problem dabei: Die Kiste ist ein HP mit einem hübschen Windows-XP-Lizenzaufkleber (OEM-Lizenz), als CD habe ich aber nur eine normale Verkaufsversion („Retail“) von Windows XP zur Verfügung. Und wenn man mit der installiert, dann wird der Lizenzcode als nicht gültig zurückgewiesen.

Google gibt einem sehr viele Tipps, wie man die Installations-CD „umbauen“ kann, aber das wollte ich nicht (zumal XP ja schon installiert war). Am Ende fand sich dann ein extrem einfacher Weg und das auch noch ausschließlich mit Windows / Microsoft-Bordmitteln:

1. Schritt 1 ist die Installation von Windows XP mit der Retail-CD ganz normal wie immer – die Frage mit dem Lizenzschlüssel kann man (zumindest bei einer SP3-CD) einfach überspringen. Man erhält dann ein System, das im 30-Tage-Testmodus ist
2. Nun geht man auf <http://windows.microsoft.com/de-DE/windows/help/genuine/product-key> und wählt oben den Punkt *„Windows XP“*
3. Dort folgt man den Schritten, die unten unter *„So aktualisieren Sie Ihren Product Key“* beschrieben werden – man lädt also das *„Windows-Aktualisierungstool für Product Keys“*, startet es und gibt seinen OEM-Lizenz-Code vom Aufkleber ein
4. Das war es schon! Die Lizenz wird eingetragen und auch gleich aktiviert

Das Tool prüft (wie auch immer), dass es sich um keine Raubkopie handelt, aber darum soll es hier auch nicht gehen.