# Einträge (Posts)
Die API Endpoints die zum abrufen der Posts im Blog, News und Podcastbereich verwendet werden.

Inhalt dieser Datei:

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

# Index
## GET /app/posts/blog.json
Eine Liste von Posts im Blog inklusive Content.

Autorisierung nicht erforderlich.
Alternativ ist es über `GET /blog.json` möglich blogposts und news in einem Feed zu erhalten, allerdings ist es für die meisten Anwendungen nicht Wünschenswert.

#### Anmerkung zu 1UP Posts
Posts bei denen `subscription_only` auf `true` steht sind zwar für alle lesbar, die IDs für Mediendateien werden allerdings nicht mitgeschickt sofern der User kein Abonnement hat.
Ob der User ein Abonnement hat kann sowohl über `GET /users/me.json` in [Login und Sessions](/LPRodney/g1api-docs/src/master/api_doc/login.md) bereits beim Start überprüft und gespeichert werden oder anhand des `subscription` booleans innerhalb der Antwort überprüft werden.
### Parameter

| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `page` | Nein | Integer | Seite |
| `per_page` | Nein | Integer | Items pro Seite (Standard: 8 [iOS], 20 [Android]) |

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/posts/blog.json?page=1&per_page=8'
```

### Beispielantwort
```json
{
	"items": [{
		"post": {
			"cached_rating": 4.5455,
			"excerpt": "Und das war’s!",
			"id": 1364365,
			"post_type": "blog",
			"published_at": "2014-09-23T17:30:00+02:00",
			"title": "GameArt-Contest: Eure Motive zur 300",
			"body": "<p><strong>Update vom 23. September:</strong></p>\n<p>So, der Contest ist durch! Bis zum TV-Start von Folge 300 am Ende der Woche werden wir das Gewinnermotiv wählen und hier veröffentlichen. Vielen Dank für euer großes Interesse und eure Einsendungen!</p>\n<p><strong>Ursprünglicher Blogpost:</strong></p>\n<p>Freunde, wir haben es fast geschafft &#8211; 300 Folgen Game One. Wie krass ist das denn?! Und anlässlich dieser großartigen Neuigkeit gibt’s hier mal wieder einen feinen Contest für die künstlerisch Begabten unter euch: <strong>Schickt uns via Upload-Möglichkeit unten ein Motiv, das 300 Folgen Game One angemessen zelebriert.</strong> Und kommt uns nicht mit einem Motiv im Stil des Films &#8220;300&#8221; um die Ecke. So schlau waren wir auch schon. Es muss nicht mal die Zahl 300 auftauchen. Überrascht und begeistert uns.</p>\n<p>Das Gewinner-Motiv wird dann tatsächlich auf einem Shirt verewigt, das in unserem Shop angeboten wird. Und der Designer dieses Motivs bekommt natürlich auch noch was, nämlich ein signiertes Shirt und noch ein Goodie-Paket. Cool? Cool!</p>\n<p>PS: An alle, die immer wieder geklaute Sachen reinstellen: Lasst es einfach! Es wird spätestens von der Community in den Comments aufgedeckt und anschließend gelöscht. Inspirieren lassen ist okay, aber wer einfach was runterlädt und als sein Eigentum ausgibt, handelt nicht nur unfair allen anderen Teilnehmern gegenüber, sondern macht sich auch strafbar im Sinne des Urheberrechts. Außerdem sind wir rechtlich verpflichtet, euch darauf hinzuweisen, dass ihr keine Gewinnbeteiligung oder Rechte an dem Motiv besitzt, sobald ihr es hier in dem Contest eingereicht habt. Natürlich werden wir aber in der Produktbeschreibung euren Namen als Designer des Produktes angeben &#8211; sofern ihr das wünscht.</p>",
			"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/695/blog_list/Teaser_Game_Art_300.jpg",
			"tags_string": "300, GameArt, Motiv",
			"games_string": "",
			"ratings_count": 11,
			"comments_count": 22,
			"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/695/editorial_thumb/Teaser_Game_Art_300.jpg",
			"categories_string": "unplugged",
			"author": {
				"id": 51573,
				"name": "Redaktion",
				"avatar_image_url": "http://www.gravatar.com/avatar/a0fc73649a3d0710b5b62e3c728a47e9?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
			},
			"subscription_only": false,
			"share_url": "https://gameone.de/blog/2014/9/gameart-contest-dein-motiv-zur-300",
			"target_url": "https://gameone.de/blog/2014/9/gameart-contest-dein-motiv-zur-300"
		}
	},
	{
		"post": {
			...
		}
	},
	...
	],
	"total_entries": 1870,
	"total_pages": 234,
	"current_page": 1,
	"per_page": 8,
	"subscription": false
}
```
-----------------------
## GET /app/posts/news.json
Eine Liste von Posts im News Bereich inklusive Content.

Autorisierung nicht erforderlich.
Alternativ ist es über `GET /blog.json` möglich blogposts und news in einem Feed zu erhalten, allerdings ist es für die meisten Anwendungen nicht Wünschenswert.


| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `page` | Nein | Integer | Seite |
| `per_page` | Nein | Integer | Items pro Seite (Standard: 8 [iOS], 20 [Android]) |

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/posts/mews.json?page=1&per_page=8'
```

### Beispielantwort
```json
{
	"items": [{
		"post": {
			"cached_rating": 4.0,
			"excerpt": "Vor der T\u00fcr h\u00f6rt dich niemand schreien",
			"id": 1366159,
			"post_type": "news",
			"published_at": "2014-10-09T13:15:07+02:00",
			"title": "NEWS \"Alien: Isolation\" - Wenn T\u00fcren zum Alptraum werden",
			"body": "<p>In &#8220;Alien: Isolation&#8221; spielt ihr <em>Ellens</em> Tochter <em>Amanda Ripley</em>, die sich auf der Raumstation Sevastopol mit einem grimmigen Alien herumschlagen muss, das ziemlich unentspannt auf jedwedes menschliches Leben reagiert. Offenbar lauern in dem verlassenen Blechk\u00fcbel aber noch ganz andere Gefahren &#8211; Gefahren, gegen die der Xenomorph anscheinend ziemlich abkackt.</p>\n<p>Durch einen lustigen Bug f\u00e4llt es <em>Amanda</em> sichtbar schwer, sich einer bestimmten T\u00fcr zu n\u00e4hern. Sobald sie doch in die N\u00e4he des eigentlich friedlich aussehenden Schotts geht, schreckt sie angsterf\u00fcllt und keuchend zur\u00fcck. Was k\u00f6nnte sich wohl hinter der T\u00fcr verstecken? F\u00fchrt die Luke vielleicht etwa direkt an den Anfang von &#8220;Aliens: Colonial Marines&#8221;?</p>\n<video src=\"youtube://www.youtube.com/watch?v=lY2EBIqtPng\"></video>\n<p><a href=\"http://de.ign.com/alien-isolation-xbox-360/99648/news/amanda-ripley-hat-eine-tur-phobie\">Quelle</a></p>",
			"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/857/blog_list/alien_isolation_teaser6.jpg",
			"tags_string": "alien isolation, creative assembly, johannes",
			"games_string": "Alien: Isolation",
			"ratings_count": 6,
			"comments_count": 9,
			"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/857/editorial_thumb/alien_isolation_teaser6.jpg",
			"categories_string": "",
			"author": {
				"id": 205588,
				"name": "Johannes",
				"avatar_image_url": "http://www.gravatar.com/avatar/0a54c599190942ba3915b1d1d89a34ad?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
			},
			"share_url": "https://gameone.de/news/2014/10/alien-isolation-wenn-tueren-zum-alptraum-werden",
			"target_url": "https://gameone.de/news/2014/10/alien-isolation-wenn-tueren-zum-alptraum-werden"
		}
	},
	{
		"post": {
			...
		}
	},
	...
	],
	"total_entries": 1586,
	"total_pages": 80,
	"current_page": 1,
	"per_page": 20,
	"subscription": true
}
```
-----------------------
## GET /app/posts/podcast.json
Der Podcastfeed der in der App verwendet wird.

Autorisierung nicht erforderlich.

#### Anmerkung zu 1UP Posts
Posts bei denen `subscription_only` auf `true` steht sind zwar für alle lesbar, die IDs für Mediendateien werden allerdings nicht mitgeschickt sofern der User kein Abonnement hat.
Ob der User ein Abonnement hat kann sowohl über `GET /users/me.json` in [Login und Sessions](/LPRodney/g1api-docs/src/master/api_doc/login.md) bereits beim Start überprüft und gespeichert werden oder anhand des `subscription` booleans innerhalb der Antwort überprüft werden.
### Parameter

| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `page` | Nein | Integer | Seite |
| `per_page` | Nein | Integer | Items pro Seite (Standard: 8 [iOS], 20 [Android]) |

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/posts/podcast.json?page=1&per_page=8'
```

### Beispielantwort
```json
{
	"items": [{
		"post": {
			"cached_rating": 5.0,
			"excerpt": "Modern Talking",
			"id": 1366162,
			"post_type": "podcast",
			"published_at": "2014-10-09T16:50:57+02:00",
			"title": "Appklusiv: AppCast #235",
			"body": "<p>Es ist Donnerstag Nachmittag und hier ist der AppCast mit der Nummer 235. Auch heute wieder pr\u00e4sentiert von unserem flotten Turbo-Duo, bestehend aus dem herzlichen Hauke und dem jecken Johannes.</p>\n<p>Lauscher auf und durch!</p>\n<p>AppCast#235 (30:33 Minuten)<br />\n<video src=\"rtaudio:791\"></video></p>",
			"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/860/blog_list/Teaser_Appcast_235.jpg",
			"tags_string": "appklusiv, appcast, 235, hauke, johannes",
			"games_string": "",
			"ratings_count": 1,
			"comments_count": 4,
			"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/860/editorial_thumb/Teaser_Appcast_235.jpg",
			"categories_string": "",
			"author": {
				"id": 205588,
				"name": "Johannes",
				"avatar_image_url": "http://www.gravatar.com/avatar/0a54c599190942ba3915b1d1d89a34ad?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
			},
			"subscription_only": true,
			"share_url": "https://gameone.de/blog/2014/10/appklusiv-appcast-235",
			"target_url": "https://gameone.de/blog/2014/10/appklusiv-appcast-235"
		}
	},
	{
		"post": {
			...
		}
	},
	...
	],
	"total_entries": 361,
	"total_pages": 19,
	"current_page": 1,
	"per_page": 20,
	"subscription": true
}
```
-----------------------
## GET /app/blog/premium.json
Eine Liste von "Appklusiven" Posts inklusive Content

Liste kann ohne Autorisierung abgerufen werden.

Autorisierung und 1UP Abonnement für kompletten Inhalt der Posts inklusive Medien-IDs erforderlich.


### Parameter

| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `page` | Nein | Integer | Seite |
| `per_page` | Nein | Integer | Items pro Seite (Standard: 8 [iOS], 20 [Android]) |

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/blog/podcast.json?page=1&per_page=8'
```

### Beispielantwort
```json
{
	"items": [{
		"post": {
			"cached_rating": 5.0,
			"excerpt": "Sooo lustig!",
			"id": 1366199,
			"post_type": "blog",
			"published_at": "2014-10-10T10:30:00+02:00",
			"title": "Appklusive Outtakes zur Folge 301",
			"body": "<p>Auch beim Dreh unserer neuesten Folge gab\u2019s unfreiwillig wieder viel zu lachen. Besonders Krys verabschiedet sich mit einer sagenhaft komischen Performance. Viel Spa\u00df beim Anschauen!</p>",
			"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/005/blog_list/outtakes_289.jpg",
			"tags_string": "outtakes, 301",
			"games_string": "",
			"ratings_count": 11,
			"comments_count": 8,
			"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/005/editorial_thumb/outtakes_289.jpg",
			"categories_string": "unplugged",
			"author": {
				"id": 101359,
				"name": "Fabian",
				"avatar_image_url": "http://www.gravatar.com/avatar/dbe163ff83f8dde6f346f1c8d207bda7?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
			},
			"subscription_only": true,
			"share_url": "https://gameone.de/blog/2014/10/appklusive-outtakes-zur-folge-301",
			"target_url": "https://gameone.de/blog/2014/10/appklusive-outtakes-zur-folge-301"
		}
	},
	{
		"post": {
			...
		}
	},
	...
	],
	"total_entries": 474,
	"total_pages": 24,
	"current_page": 1,
	"per_page": 20,
	"subscription": false
}
```
-----------------------

## GET /tv.json
Ruft eine Liste der TV Episoden ab. Der erste Eintrag ist jeweils die neuste Folge.

Liste kann ohne Autorisierung abgerufen werden.

#### Anmerkung zu 1UP Episoden
Episoden bei denen `subscription_only` auf `true` steht sind zwar für alle lesbar, die IDs für Mediendateien werden allerdings nicht mitgeschickt sofern der User kein Abonnement hat.
Ob der User ein Abonnement hat kann sowohl über `GET /users/me.json` in [Login und Sessions](/LPRodney/g1api-docs/src/master/api_doc/login.md) bereits beim Start überprüft und gespeichert werden oder anhand des `subscription` booleans innerhalb der Antwort überprüft werden.

### Parameter

| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `page` | Nein | Integer | Seite |
| `per_page` | Nein | Integer | Items pro Seite (Standard: 8 [iOS], 20 [Android]) |

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/tv.json?page=1&per_page=8'
```

### Beispielantwort
```json
{
	"items": [{
		"tv_show": {
			"air_date": "2014-10-07",
			"air_year": 2014,
			"cached_rating": 4.45,
			"episode": 301,
			"id": 355,
			"long_description": "<p>Puh, Folge eins nach dem dicken One-Shot-Jubil\u00e4um. Und da stehen einige gro\u00dfe Titel an! Zuerst brettert Greg durch &#8220;Forza Horizon 2&#8221;, dann teilt Tim seine Eindr\u00fccke zu &#8220;Super Smash Bros. 3DS&#8221; mit euch. Preisbewusst geht\u2019s anschlie\u00dfend nach &#8220;Mittelerde&#8221;, wo sich Fabian in &#8220;Mordors Schatten&#8221; gesonnt hat. Den Abschluss macht schlie\u00dflich noch mal Gregor, der euch &#8220;D4: Dark Dreams Don\u2019t Die&#8221; pr\u00e4sentiert.</p>",
			"published_at": "2014-10-10T21:20:00+02:00",
			"short_description": "Forza Horizon 2, Super Smash Bros. 3DS, Mittelerde: Mordors Schatten, D4: Dark Dreams Don't Die",
			"total_views": 79384,
			"title": "Game One - Folge 301",
			"preview_image": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/645/983/big/640x360.jpg",
			"video_url": "http://videos.mtvnn.com/de7daca39e48eca6d6769dafba28d8e2.m3u8",
			"games_string": "",
			"ratings_count": 218,
			"duration": 1304.23,
			"comments_count": 123,
			"small_image_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/645/983/medium/640x360.jpg",
			"subscription_only": false,
			"share_url": "https://gameone.de/tv/301",
			"target_url": "https://gameone.de/tv/301"
		}
	},
	{
		"post": {
			...
		}
	},
	...
	],
	"total_entries": 301,
	"total_pages": 16,
	"current_page": 1,
	"per_page": 20,
	"subscription": true
}
```

-----------------------
# Posts
## GET /app/posts/<post_type>/<id>.json
Valide Werte für post_type 
| post_type | Beschreibung |
| --------- | ------------ |
| blog | Blogeintrag |
| news | Newsbeitrag |
| podcast | Podcast Episode |

Im index ist `post_type` in jedem Objekt enthalten. (Außnahme ist der TV-Index)

Autorisierung nicht erforderlich.

Dieser Request hat keine Parameter.

#### Anmerkung zu 1UP Posts
Posts bei denen `subscription_only` auf `true` steht sind zwar für alle lesbar, die IDs für Mediendateien werden allerdings nicht mitgeschickt sofern der User kein Abonnement hat.
Ob der User ein Abonnement hat kann sowohl über `GET /users/me.json` in [Login und Sessions](/LPRodney/g1api-docs/src/master/api_doc/login.md) bereits beim Start überprüft und gespeichert werden oder anhand des `subscription` booleans innerhalb der Antwort überprüft werden.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/posts/blog/1365875.json'
```

```json
{
	"post": {
		"cached_rating": 4.625,
		"excerpt": "Kommen drei Helden in einen Dungeon...",
		"id": 1365875,
		"post_type": "blog",
		"published_at": "2014-10-09T11:00:00+02:00",
		"title": "1 Beutezeug mit Gauntlet",
		"body": "<p>Warner hat mit &#8220;Gauntlet&#8221; einen richtigen Videospiel-Oldie reanimiert. In dem bei <a href=\"http://store.steampowered.com/app/258970/?l=german\">Steam</a> f\u00fcr knapp 20 Euro erh\u00e4ltlichen Titel pr\u00fcgelt und zaubert ihr euch mit bis zu drei Freunden durch allerlei monsterverseuchte Dungeons. Wenn ihr das Konzept von &#8220;Gauntlet&#8221; nicht kennt, stellt es euch einfach als eine Art (noch) simpleres &#8220;Diablo&#8221; vor. Aktuell ist das Spiel exklusiv f\u00fcr den PC erh\u00e4ltlich, \u00fcber baldige Konsolen-Ports w\u00fcrden wir uns aber nicht wundern. Hier nun unsere halbst\u00fcndige &#8220;Runde mit&#8221;, f\u00fcr die sich Dennis, Etienne und Johannes auf der Couch eingefunden haben.</p>\n<video src=\"riptide:a74ce5cd3a02d76ffe8896c2bd7adc78\"></video>\t\n<p>Als Bonus bekommt ihr hier noch ein vor dem Release des Spiels gef\u00fchrtes Videointerview mit Rob Tatnell, Art Director bei Entwickler Arrowhead:</p>\n<video src=\"riptide:fb26b7baa31b90874c885a6d855358e4\"></video>\t\n<p>Was haltet ihr von Warners Kerkerklopper?</p>",
		"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/821/blog_list/gauntlet_eine_runde_mit.jpg",
		"tags_string": "1 runde mit, gauntlet, pc, dennis, etienne, johannes",
		"games_string": "",
		"ratings_count": 16,
		"comments_count": 19,
		"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/821/editorial_thumb/gauntlet_eine_runde_mit.jpg",
		"categories_string": "games",
		"author": {
			"id": 101359,
			"name": "Fabian",
			"avatar_image_url": "http://www.gravatar.com/avatar/dbe163ff83f8dde6f346f1c8d207bda7?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
		},
		"subscription_only": false,
		"share_url": "https://gameone.de/blog/2014/10/1-beutezeug-mit-gauntlet",
		"target_url": "https://gameone.de/blog/2014/10/1-beutezeug-mit-gauntlet"
	}
}
```
-----------------------
## GET /tv/<episode>.json 
<episode> ist die Episodennummer im key `episode` zu finden in jedem tv_show Objekt des Indexes.

Autorisierung nicht erforderlich, allerdings wird die Medien-ID bei nicht vorhandenem 1UP Abonnement nicht mitgesendet.

#### Anmerkung zu 1UP Episoden
Episoden bei denen `subscription_only` auf `true` steht sind zwar für alle lesbar, die IDs für Mediendateien werden allerdings nicht mitgeschickt sofern der User kein Abonnement hat.
Ob der User ein Abonnement hat kann sowohl über `GET /users/me.json` in [Login und Sessions](/LPRodney/g1api-docs/src/master/api_doc/login.md) bereits beim Start überprüft und gespeichert werden oder anhand des `subscription` booleans innerhalb der Antwort überprüft werden.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/app/posts/blog/1365875.json'
```

```json
{
	"tv_show": {
		"air_date": "2014-09-16",
		"air_year": 2014,
		"cached_rating": 4.42,
		"episode": 299,
		"id": 353,
		"long_description": "<p>Knuddelbunt geht\u2019s in dieser Folge los mit Gregor Beitrag zum 3DS-Epos &#8220;Fantasy Life&#8221;. Danach verkehrt sich die Stimmung ins Gegenteil, denn in Haukes Beitrag zu &#8220;Wasteland 2&#8221; wird\u2019s ernst und ruppig. Danach feiern wir wieder ein Jubil\u00e4um und werfen einen umfassenden Blick auf das Genre Echtzeit-Strategie. Auch dieser Beitrag stammt von Gregor &#8211; verr\u00fcckt.</p>",
		"published_at": "2014-09-19T21:30:00+02:00",
		"short_description": "Fantasy Life, Wasteland 2, Happy Birthday Echtzeit-Strategie",
		"total_views": 155971,
		"title": "Game One - Folge 299",
		"preview_image": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/645/517/big/640x360.jpg",
		"video_url": "http://videos.mtvnn.com/7ceff0a975e940400337cceca48bbfd9.m3u8",
		"games_string": "",
		"ratings_count": 242,
		"duration": 1312.19,
		"comments_count": 121,
		"small_image_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/645/517/medium/640x360.jpg",
		"subscription_only": false,
		"share_url": "https://gameone.de/tv/299",
		"target_url": "https://gameone.de/tv/299",
		"blog_posts": [],
		"games": []
	}
}
```

-----------------------
# Objekte
## post
Das `post` Objekt wird für Blogeinträge, Podcasts und Newsbeiträge verwendet.
Die Struktur ist immer die selbe.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"post": {
		"cached_rating": 4.625, # Float der die durchschnittliche Bewertung des Posts (0-5) darstellt.
		"excerpt": "Kommen drei Helden in einen Dungeon...", # Untertitel im Blog
		"id": 1365875, # ID des Posts
		"post_type": "blog", # post_type (siehe oben)
		"published_at": "2014-10-09T11:00:00+02:00", # Veröffentlichungszeitpunkt
		"title": "1 Beutezeug mit Gauntlet", # Titel
		"body": "*snip*", # Body enthält den Post als HTML, dieser Enthält ggf. Mediendateien, siehe die Dokumentation für Medien für mehr Informationen
		"image_url": "http://s3.gameone.de/gameone/assets/images/000/008/821/blog_list/gauntlet_eine_runde_mit.jpg", # Teaser-Bild im Blog bzw. der Übersicht
		"tags_string": "1 runde mit, gauntlet, pc, dennis, etienne, johannes", # Tags
		"games_string": "", # ggf. Referenzierte Spiele, kommaseperierter String
		"ratings_count": 16, # Anzahl der Bewertungen
		"comments_count": 19, # Anzahl der Kommentare
		"small_image_url": "http://s3.gameone.de/gameone/assets/images/000/008/821/editorial_thumb/gauntlet_eine_runde_mit.jpg", # kleinere Version des Teaserbildes
		"categories_string": "games", # Kategorie(n), kommaseperierter String
		"author": {
			"id": 101359, # User-id des Autors
			"name": "Fabian", # Username des Autors
			"avatar_image_url": "*snip*" # Link zum Gravatar-Avatar des Autors
		},
		"subscription_only": false, # Definiert ob der Post "Appklusiv" ist
		"share_url": "https://gameone.de/blog/2014/10/1-beutezeug-mit-gauntlet", # URL auf der Website, genutzt wenn die "Teilen" Funktion der App genutzt wird
		"target_url": "https://gameone.de/blog/2014/10/1-beutezeug-mit-gauntlet" # ???
	}
}
```

## tv_show
Das `tv_show` Objekt wird für TV-Episoden verwendet.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"tv_show": {
		"air_date": "2014-04-22", # Veröffentlichungsdatum (App)
		"air_year": 2014, # Veröffentlichungsjahr
		"cached_rating": 4.34, # Durchschnittliche Bewertung
		"episode": 285, # Episodennnummer.
		"id": 339, # ID (ungenutzt)
		"long_description": "*snip*", # Vollständige Beschreibung
		"published_at": "2014-04-25T21:00:00+02:00", # Veröffentlichungszeitpunkt (Website/TV)
		"short_description": "LEGO The Movie, GBA-Special, Turbo Duo, Mr. Rabatto: Smash Hit", # Kurze Beschreibung/Untertitel
		"total_views": 131396, # Anzahl der Aufrufe
		"title": "Game One - Folge 285", # Titel
		"preview_image": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/643/500/big/640x360.jpg", # Thumbnail
		"video_url": "http://videos.mtvnn.com/53535182bfad65320a5ba2d569721424.m3u8", # URL für den HLS Stream, siehe die Dokumentation für Medien für mehr Informationen
		"games_string": "", # Kommaseperierter String der vorkommenden Spiele (ungenutzt)
		"ratings_count": 250, # Anzahl der Bewertungen
		"duration": 1230.42, # Länge in Sekunden als Float
		"comments_count": 161, # Anzahl der Kommentare
		"small_image_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/643/500/medium/640x360.jpg", # kleines Thumbnail
		"subscription_only": false, # Definiert ob die Episode "Appklusiv" ist
		"share_url": "https://gameone.de/tv/285", # URL auf der Website, genutzt wenn die "Teilen" Funktion der App genutzt wird
		"target_url": "https://gameone.de/tv/285", # ???
		"blog_posts": [], # ??? (ungenutzt)
		"games": [] # Array der vorkommenden Spiele (ungenutzt)
	}
}
```