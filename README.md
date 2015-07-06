# THIS DOCUMENTATION IS IN GERMAN AND WON'T BE UPDATED ANYMORE
# IT'S INCOMPLETE AND DESIGNED FOR BITBUCKET'S MARKDOWN AND MIGHT LOOK TERRIBLE ON HERE
# I PUT IT HERE BECAUSE FUCK IT

#Unofficial Game One API Documentation
Hier soll einmal eine (fast) vollständige Dokumentation der GameOne.de API die von den iOS/Android Apps genutzt wird ein Zuhause finden.

##Übersicht
Die Game One API verwendet mit wenigen ausnahmen JSON.
Die Requests and die API erfordern bestimmte Header damit diese vom Server direkt auf die homepage weitergeleitet werden.

Nicht dokumentiert sind die API Enpoints die beim abschließen eines 1UP Abonnements verwendet werden.

### ToDo
 * News, Podcast und "Appklusiv" Posts
 * Playtube
 * Mediendateien (Audio, Video, Gallerien) - Metadaten und die Dateien selbst abrufen
 * Suche (Allgemeine und spezifische [Blog, News, Playtube, etc.])
 * "Games" Kategorie

### Header

Die von der iOS App verwendeten Header sind (Version 2.0.2), alles hinter `#` sind Kommentare:
```bash
User-Agent: GameOne/345 CFNetwork/609 Darwin/13.0.0 # User-Agent der aktuellen version
X-G1APP-DEVICEINFO: iPhone3,1_6.0 # Gerätetyp, in meinem Fall ein iPhone 4 unter iOS 6.0
X-G1APP-IDENTIFIER: EB9BC720D85B67C3A66AA71C37105C98 # der Identifier der App, zufällig generiert
X-G1APP-VERSION: 2.0.2(345) # Die Version der app
X-G1APP-APPIDENTIFIER: de.gameone.iphone # Der Identifier der App
Authorization: Basic dGVzdDp0ZXN0= # HTTP Basic Authentication
```
Die von der Android App verwendeten Header sind (Version 2.0), alles hinter `#` sind Kommentare:
```bash
User-Agent: GameOne/Android
X-G1APP-IDENTIFIER: f6db8352-09c6-4cb5-bddd-751b9d25c19d # identifier im UUID format
X-G1APP-VERSION: 93
X-G1APP-DEVICEINFO: LGE_Nexus-5_4.4.4
Authorization: Basic dGVzdDp0ZXN0=
```
Für einen Request erforderlich sind lediglich `X-G1APP-IDENTIFIER` und der User-Agent.
Der Wert für `X-G1APP-IDENTIFIER` ist egal, im Beispiel verwende ich nur `x`. Beim User-Agent gilt das dieser `GameOne` enthalten muss, der Rest ist ebenfalls egal.
Der Authorizazion Header kann weggelassen werden, da Cookies unterstützt werden. Diese müssen allerdings ggf. erneuert werden.

Beispiel eines Requests für die Blogeinträge:
```bash
$ curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' 'https://gameone.de/app/posts/blog.json?&page=1&per_page=8'
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Status: 200
X-Powered-By: Phusion Passenger (mod_rails/mod_rack) 3.0.18
Cache-Control: max-age=0, no-cache, no-store
X-UA-Compatible: IE=Edge,chrome=1
Set-Cookie: _mtvnn-gameone-r3_session=f1orsbbvmmfl8qinccykypzdhszga8jv; domain=.gameone.de; path=/; HttpOnly
X-Request-Id: b18dedf2fc36a7f287c739be50b4f632
X-Runtime: 0.056801
Date: Wed, 24 Sep 2014 14:39:22 GMT
X-Rack-Cache: miss
Server: nginx/1.2.1 + Phusion Passenger 3.0.18 (mod_rails/mod_rack)

{"items": ...}
```
### Error/Fehlermeldungen
Die API gibt bei Fehlern meistens keine Meldung im JSON Format zurück. Entweder ein HTTP Fehlercode oder die Gameone.de 404-Seite.

-----------------------
## Index

### [Login, Sessions und User](/LPRodney/g1api-docs/src/master/api_doc/login.md)

**API-Endpoints:**

| Endpoint | Beschreibung |
| -------- | ------------ |
| POST /session.json | Endpoint für login |
| GET /users/me.json | Die Informationen über den aktuell eingeloggten User |
| GET /users/<id>.json | Die Informationen über einen anderen User abrufen |

**Erklärungen zu keys in Objekten:**

| Objekt | Beschreibung |
| ------ | ------------ |
| user (login) | User Objekt erhatlten beim Login |
| user (me) | User Objekt des eingeloggten User |
| user (anderer) | User Objekt eines anderen Users |

### [Posts](/LPRodney/g1api-docs/src/master/api_doc/posts.md)

**Index:**

| Endpoint | Beschreibung |
| -------- | ------------ |
| GET /app/posts/blog.json | Ruft Blogeinträge ab |
| GET /app/posts/news.json | Ruft News ab |
| GET /app/posts/podcast.json | Ruft den Podcast feed ab |
| GET /app/blog/premium.json | Ruft Appklusive Posts ab |
| GET /tv.json | Ruft Liste der TV Folgen ab |

**Posts:**

| Endpoint | Beschreibung |
| -------- | ------------ |
| GET /app/posts/<post_type>/<id>.json | Ruft Blogpost von Typ <post_type> mit id <id> ab |
| GET /tv/<episode>.json | Ruft die Daten zu TV-Episode <episode> ab |

**Erklärungen zu keys in Objekten:**

| Objekt | Beschreibung |
| ------ | ------------ |
| post | Blog-/Newseintrag oder Podcast |
| tv_show | TV-Episode |

### [Medien](/LPRodney/g1api-docs/src/master/api_doc/media.md)
**Metadaten:**

| Endpoint | Beschreibung |
| -------- | ------------ |
| GET /videos/<id>.json | Metadaten von Videos |
| GET /audios/<id>.json | Metadaten von Audiodateien |
| GET /galleries/<id>.json | Metadaten von Bildergallerien |

**Mediendateien:**

| Endpoint | Beschreibung |
| -------- | ------------ |
| GET https://videos.mtvnn.com/android/videos/<id>.json | Videodateien (Legacy, Android SDK Version < 11) |
| GET <video_url> / <iphone_url> | Videostreams (HLS) |

**Erklärungen zu keys in Objekten:**

| Objekt | Beschreibung |
| ------ | ------------ |
| video_meta | Metadaten von Videodateien |
| audio_meta | Metdaten von Audiodateien |
| gallery | Gallerien |

### Misc (Suche, Kommentare, etc.)
-----------------------

### Playtube
Coming Soon™...