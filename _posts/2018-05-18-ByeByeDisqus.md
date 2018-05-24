---
layout: post
title: Bye bye Disqus....
categories: [Allgemein, Blog]
comments: true
---

Die DSGVO rückt immer näher. Weil ich blogmäßig auf Jekyll umgestiegen bin, dachte ich es sei ja kein Problem. Keine Cookies, keine Fremdanfragen, nur gute alte statische Websites mit Hyperlinks. Tja, denkste!<!--more-->

Nachdem ich einen Blogpost mit Disqus-Einbindung über die Website [https://webbkoll.dataskydd.net/en](https://webbkoll.dataskydd.net/en) geprüft habe, wurden mir nicht weniger als **28 Cookies** sowie viele weitere Fremd-Aufrufe angezeigt - darunter auch Links zu Werbefirmen, Facebook Statistiken und Google APIs. Das ist leider nicht mehr tragbar.

Aus diesem Grund, habe ich die Kommentare mit Disqus wieder entfernt. Die Seite ist nun wieder **statisch**, benutzt **keine Cookies** und erfasst auch sonst keine [Personenrelevanten Daten](https://webbkoll.dataskydd.net/en/results?url=http%3A%2F%2Fmarcelcremer.github.io%2FAsync_server%2F).

Es werden lediglich abgeholt:
- Fontawesome per CDN
- Mein Avatar, direkt hier von Github

Für alle, die wissen wollen, was das Disqus-Plugin so ausgelöst hat:

``` text
use.fontawesome.com (https://use.fontawesome.com/releases/v5.0.10/css/a...)
avatars3.githubusercontent.com (https://avatars3.githubusercontent.com/u/6123724?s...)
https-marcelcremer-github-io.disqus.com (https://https-marcelcremer-github-io.disqus.com/em...)
use.fontawesome.com (https://use.fontawesome.com/releases/v5.0.10/webfo...)
use.fontawesome.com (https://use.fontawesome.com/releases/v5.0.10/webfo...)
disqus.com (https://disqus.com/next/config.js)
c.disquscdn.com (https://c.disquscdn.com/next/embed/styles/lounge.1...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/common.bundle.0...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/lounge.bundle.2...)
disqus.com (https://disqus.com/embed/comments/?base=default&f=...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/lounge.load.b4a...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/common.bundle.0...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/styles/lounge.1...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/lounge.bundle.2...)
disqus.com (https://disqus.com/next/config.js)
c.disquscdn.com (https://c.disquscdn.com/next/current/embed/lang/de...)
ssl.google-analytics.com (https://ssl.google-analytics.com/ga.js)
c.disquscdn.com (https://c.disquscdn.com/next/embed/assets/img/load...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/styles/discover...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/assets/img/spri...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/alfalfa.4a5fcca...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/assets/font/ico...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/assets/img/noav...)
c.disquscdn.com (https://c.disquscdn.com/next/embed/discovery.bundl...)
cdn.viglink.com (https://cdn.viglink.com/images/pixel.gif?ch=1&rn=1...)
cdn.viglink.com (https://cdn.viglink.com/images/pixel.gif?ch=2&rn=1...)
connect.facebook.net (https://connect.facebook.net/en_US/sdk.js)
apis.google.com (https://apis.google.com/js/api.js)
disqus.com (https://disqus.com/api/3.0/discovery/listRelated.j...)
www.facebook.com (https://www.facebook.com/impression.php/f35564e7b7...)
staticxx.facebook.com (https://staticxx.facebook.com/connect/xd_arbiter/r...)
www.facebook.com (https://www.facebook.com/connect/ping?client_id=52...)
apis.google.com (https://apis.google.com/_/scs/apps-static/_/js/k=o...)
staticxx.facebook.com (https://staticxx.facebook.com/connect/xd_arbiter/r...)
accounts.google.com (https://accounts.google.com/o/oauth2/iframe#origin...)
ssl.gstatic.com (https://ssl.gstatic.com/accounts/o/3723580519-idpi...)
accounts.google.com (https://accounts.google.com/o/oauth2/iframerpc?act...)
glitter.services.disqus.com (https://glitter.services.disqus.com/urls/?callback...)
ssl.google-analytics.com (https://ssl.google-analytics.com/r/__utm.gif?utmwv...)
links.services.disqus.com (https://links.services.disqus.com/api/ping)
referrer.disqus.com (https://referrer.disqus.com/juggler/event.gif?abe=...)
live.rezync.com (https://live.rezync.com/pixel.html?c=4656c20ee3521...)
ib.adnxs.com (https://ib.adnxs.com/getuid?https%3A%2F%2Fs.cpx.to...)
io.narrative.io (https://io.narrative.io/?companyId=19&id=disqus_id...)
pippio.com (https://pippio.com/api/sync?pid=1391&ref=https%3A%...)
links.services.disqus.com (https://links.services.disqus.com/api/domains)
ib.adnxs.com (https://ib.adnxs.com/bounce?%2Fgetuid%3Fhttps%253A...)
s.cpx.to (https://s.cpx.to/ca.png?ref=&pid=12037&url=https%3...)
idsync.rlcdn.com (https://idsync.rlcdn.com/462246.gif?partner_uid=c6...)
cm.g.doubleclick.net (https://cm.g.doubleclick.net/pixel?google_nid=pipp...)
dc.arrivalist.com (https://dc.arrivalist.com/px/?pixel_id=1405&event_...)
pixel.sojern.com (https://pixel.sojern.com/idSync/sync?pid=arbor)
ib.adnxs.com (https://ib.adnxs.com/getuid?https%3A%2F%2Fs.cpx.to...)
rc.rlcdn.com (https://rc.rlcdn.com/449266.gif?&n=4)
rc.rlcdn.com (https://rc.rlcdn.com/449266.gif?&n=3)
rc.rlcdn.com (https://rc.rlcdn.com/449266.gif?&n=5)
pippio.com (https://pippio.com/api/sync/ddp?pid=2&m=CO8KEhoKFg...)
s.cpx.to (https://s.cpx.to/ca.png?ref=https%3A%2F%2Fmarcelcr...)
io.narrative.io (https://io.narrative.io/?io.narrative.guid.v2=880d...)
pippio.com (https://pippio.com/api/sync?pid=4149&it=1&iv=NWFmZ...)
idsync.rlcdn.com (https://idsync.rlcdn.com/462246.gif?partner_uid=c6...)
usermatch.krxd.net (https://usermatch.krxd.net/um/v2?partner=liveramp)
secure.adnxs.com (https://secure.adnxs.com/getuid?https%3A//live.rez...)
live.rezync.com (https://live.rezync.com/sync?c=4656c20ee35215f78e9...)
beacon.krxd.net (https://beacon.krxd.net/usermatch.gif?kuid_status=...)
```