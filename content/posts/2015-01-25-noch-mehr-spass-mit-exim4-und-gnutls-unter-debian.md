---
author: sven
categories:
- Aufreger
- Crypto
- Debian
- Windows
date: "2015-01-25T21:55:58Z"
guid: http://www.gibts-doch-garnicht.de/?p=134
id: 134
title: Noch mehr Spaß mit Exim4 und GnuTLS unter Debian
url: /noch-mehr-spass-mit-exim4-und-gnutls-unter-debian/
---

Ach was eine Freude – ich hatte am Wochenende viel Spaß dabei, ein eigentlich ganz nettes Windows Phone zu konfigurieren. Dass es bei verstelltem Datum bei allen Updates und Co. durchdreht sei hier mal nur erwähnt, aber das eingebaute Mailprogramm hat mir noch mehr graue Haare beschert.

Nachdem alles richtig eingestellt war (tausendmal gegengecheckt mit Thunderbird) wollte es ums Verrecken nicht korrekt senden – die Meldung „relay not permitted“ flutete meine (seit Jahren stabile) Exim4-Konfiguration.

Ich war am verzweifeln und konnte einfach nicht verstehen, warum er überhaupt auf die Idee kam, wo doch definitiv die Haken für das Senden mit Nutzername und Passwort gesetzt waren (und es damit ja kein Relay mehr ist).

Lange Rede, kurzer Sinn: habt Ihr einen Exim-Mailserver auf dem aktuellen Stable von Debian (Stand heute 7.8), so [kompiliert ihn mal fein neu mit OpenSSL](https://www.gibts-doch-garnicht.de/e-mail-made-in-germany-und-der-standard-mailserver-von-debian-exim/ "E-Mail Made in Germany und der Standard-Mailserver von Debian (Exim)") und wie durch ein Wunder geht es dann. Seufz.

Aber Microsoft kriegt echt einen Extra-Preis – statt irgendwas im Sinne von „STARTLS geht nicht“ zu sagen wird dreist einfach so ohne Nutzer verschickt…