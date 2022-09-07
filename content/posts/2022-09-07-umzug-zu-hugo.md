---
author: sven
categories:
- Blog
date: "2022-09-07T10:17:04Z"
title: 'Umzug zu Hugo'
url: /umzug-zu-hugo/
---

Mittlerweile macht die ganze Verwaltung mittels WordPress immer weniger Spaß - erst Recht, wenn man viele davon betreibt und überall alles kompliziert manuell verwaltet werden muss (oder fast alles, ich nutze auch [MeinWP](https://mainwp.com)).

Also nach einigen anderen Seiten ist nun auch dieses Blog vom schwergewichtigen WordPress auf [Hugo](https://gohugo.io) umgestiegen. Das hat den Vorteil, dass ich nun auch die Inhalte dieses Blogs in Markdown schreiben kann und nicht mehr in WordPress' eigenem Format.

Noch besser: Das läuft alles in einer automatisierten Pipeline - ich habe alle Inhalte in [meinem GitHub-Repository](https://github.com/svenwal/gibts-doch-garnicht.de) und immer, wenn ich da eine neue Version hineinspeichere, wird automatisch die Webseite neu zusammengesetzt und mittels [Netlivy](https://www.netlify.com/) direkt veröffentlicht.

Die Migration war übrigens viel, viel einfacher als gedacht einmal mit [Wordpress to Jeykll Exporter](https://github.com/benbalter/wordpress-to-jekyll-exporter/) exortiert und dann direkt mittels [hugo import jekyll](https://gohugo.io/commands/hugo_import_jekyll/) hier eingespielt.