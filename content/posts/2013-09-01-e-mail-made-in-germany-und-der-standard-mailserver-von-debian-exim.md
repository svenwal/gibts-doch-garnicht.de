---
author: sven
categories:
- Aufreger
- Blog
- Crypto
- Debian
- Kundenverarsche
date: "2013-09-01T19:50:53Z"
guid: http://www.gibts-doch-garnicht.de/?p=93
id: 93
title: E-Mail Made in Germany und der Standard-Mailserver von Debian (Exim)
url: /e-mail-made-in-germany-und-der-standard-mailserver-von-debian-exim/
---

Na wunderbar, da haben also [unsere großen drei E-Mail-Provider GMX, web.de und Telekom endlich mal den Konfigurationsschalter gefunden](http://www.e-mail-made-in-germany.de/), um die Verbindung ([und auch nur die, nicht etwa die Mails selber…)](https://netzpolitik.org/2013/e-mail-made-in-germany-deutsche-telekom-web-de-und-gmx-machen-ssl-an-und-verkaufen-das-als-sicher/) der Mailserver zu verschlüsseln – und dann funktioniert das Ganze wohl bei vielen Standard-Debian-Mailservern nicht.

Der Grund scheint zu sein, dass Debian [wegen der Lizenz (GPL)](https://people.gnome.org/~markmc/openssl-and-the-gpl.html) nicht [OpenSSL](https://www.openssl.org/) sondern [GnuTLS](http://www.gnutls.org/) einsetzt – und dann bekommt man als Betreiber eines solchen Mailservers dann solche Einträge im Logfile:

> TLS error on connection from mout.gmx.net \[212.227.15.15\] (gnutls\_handshake): A TLS fatal alert has been received.

Für mich als Nutzer mit einem EXIM4 (heavy, gültiges SSL-Zertifikat von [StartSSL](https://www.startssl.com/)) war somit der Empfang sämtlicher Mails zumindest von GMX nicht mehr möglich (ich hatte keine Tester für web.de und Telekom zur Hand).

Man findet auch einige Einträge dazu im Netz, welche sich erstmal an diversen Konfiguratuonsänderungen versuchen (insb. in den CIPHER-Einstellungen oder gar die Deaktivierung von STARTTLS bei diesen Mailserver – kann ja auch nicht Sinn der Sache sein), am Ende läuft es darauf hinaus, dass man sich Exim4 den Source besorgt und dann seine eigene Version gelinkt gegen OpenSSL kompiliert – das funktioniert dann auch und ich bekomme wieder alle Mails 🙂

Also, was darf man in seiner Freude tun?

1. Sicherstellen, dass man einen deb-src Eintrag in seiner /etc/apt/sources aktiv hat – meiner lautet  
    > deb-src http://http.debian.net/debian stable main
    
    Nicht vergessen, ein apt-get update nachzuschieben 🙂
2. Der Anleitung unter <http://unix.stackexchange.com/questions/85231/how-to-recompile-exim4-daemon-heavy> folgen (ggf. müsst Ihr noch das eine oder andere mittels apt-get install nachinstallieren)  
    Dabei vor  
    dpkg-buildpackage -rfakeroot -us -uc  
    in der Datei debian/rules den Eintrag mit OpenSSL aktivieren: > \# If you want to build with OpenSSL instead of GnuTLS, uncomment thisOPENSSL:=1
    > 
    > \# Please note that building exim4-daemon-heavy with OpenSSL is a GPL
    > 
    > \# violation
3. Die dadurch neu entstandene .deb-Datei installieren:  
    > dpkg -i exim4-daemon-heavy\_4.80-7\_amd64.deb
    
    (oder ähnlich, Versionsnummer und Prozessorarchitektur können natürlich anders sein)
4. Sollte eigentlich sofort gehen, wenn Ihr nicht kreative Konfigurationseinträge bzgl. SSL in Eurer Exim4-Config habt.

Danke Made in Germany 🙁