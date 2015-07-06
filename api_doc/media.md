# Medien
Die API-Endpoints zum Abrufen von Metdaten und Mediendateien.

Inhalt dieser Datei:

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

# Metadaten
## GET /videos/<id>.json
Liefert die Metadaten zu einer Videoid.

Autorisierung nicht erforderlich. Es sind keine Parameter vorhanden.

### Video-IDs
Video IDs sind in Blogeinträgen innerhalb eines HTML <video> Tags zu finden, Beispiel:
```html
<video src="riptide:c97ac914655333a225cc27c92ad3c055"></video>
```

### Anmerkung für TV-Episoden und Playtube
Bei TV-Episoden muss man die Videoid aus dem `video_url` Key erhalten. Bei der Playtube besteht der Feed aus video_meta Objekten die den key `riptide_video_id` enthalten der als Wert die Video-ID hat.

Bei verwendung von HLS (siehe GET <video_url> / <iphone_url> unten) ist es nicht erforderlich die Metadaten abzurufen außer man benötigt und/oder will sie nutzen.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/videos/fb26b7baa31b90874c885a6d855358e4.json'
```

### Beispielantwort
```json
{
	"video_meta": {
		"cached_rating": 0.0,
		"created_at": "2014-06-27T11:24:07+02:00",
		"description": "Gauntlet Interview",
		"featured": false,
		"id": 644065,
		"midrolls": "",
		"riptide_id": null,
		"riptide_video_id": "fb26b7baa31b90874c885a6d855358e4",
		"title": "Gauntlet Interview",
		"img_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/644/065/big/640x360.jpg",
		"iphone_url": "http://videos.mtvnn.com/fb26b7baa31b90874c885a6d855358e4.m3u8",
		"games_string": "",
		"ratings_count": 0,
		"total_views": 0,
		"duration": 531.2,
		"comments_count": 0,
		"small_image_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/644/065/medium/640x360.jpg",
		"tags_string": "",
		"user": {
			"id": 77122,
			"name": "Bell",
			"avatar_image_url": "http://www.gravatar.com/avatar/6c9192e4d5959783b254941aa8d8e9a7?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
		}
	}
}
```
-----------------------
## GET /audios/<id>.json
Liefert die Metadaten zu einer Audio-ID.

Autorisierung nicht erforderlich. Es sind keine Parameter vorhanden.

### Audio-IDs
Audio IDs sind in Blogeinträgen innerhalb eines HTML <video> Tags zu finden, Beispiel:
```html
<video src="rtaudio:791"></video></p>
```

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/audios/791.json'
```

### Beispielantwort
```json
{
	"audio_meta": {
		"description": "AppCast #235",
		"duration": 0,
		"id": 791,
		"riptide_id": null,
		"title": "AppCast #235",
		"iphone_url": "http://s3.gameone.de/gameone/assets/audio_metas/000/000/791/original/AppCast235.mp3",
		"user": {
			"id": 205588,
			"name": "Johannes",
			"avatar_image_url": "http://www.gravatar.com/avatar/0a54c599190942ba3915b1d1d89a34ad?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png"
		}
	}
}
```
-----------------------
## GET /galleries/<id>.json
Liefert die Metadaten zu einer Gallery-ID.

Autorisierung nicht erforderlich. Es sind keine Parameter vorhanden.

### Gallerie-IDs
Gallerie IDs sind in Blogeinträgen innerhalb eines HTML <video> Tags zu finden, Beispiel:
```html
<video src="gallery:hautnah300"></video> 
```

### Anmerkung
Die Bilder sind alle im Array `images` enthalten. Die Bild-URLs sind jeweils für ein Bild der mittleren Qualitätsstufe, es ist möglich "medium" durch "large" oder auch "original" zu ersetzen und ein Bild einer höheren Auflösung zu erhalten, allerdings sollte in diesem Falle ein Fallback auf eine niedriegere Qualitätstufe vorhanden sein da nicht alle Qualitäten für alle Bilder vorhanden sind.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -X GET 'https://gameone.de/galleries/hautnah300.json'
```

### Beispielantwort
```json
{
	"gallery": {
		"active": false,
		"description": "Hautnah #300",
		"ends_at": "2014-10-01T13:43:00+02:00",
		"id": 744,
		"param": "hautnah300",
		"starts_at": "2014-10-01T13:43:00+02:00",
		"title": "Hautnah #300",
		"votable": false,
		"images": [{
			"cached_rating": 0,
			"caption": "1",
			"position": 1,
			"image_url": "http://s3.gameone.de/gameone/assets/gallery_pictures/000/018/897/medium/1.jpg"
		},
		{
			...
		},
		{
			"cached_rating": 0,
			"caption": "37",
			"position": 37,
			"image_url": "http://s3.gameone.de/gameone/assets/gallery_pictures/000/018/933/medium/37.jpg"
		}]
	}
}
```
-----------------------
# Mediendateien
## GET https://videos.mtvnn.com/android/videos/<id>.json
Dieser API Endpoint der nicht auf der gameone.de zu finden ist wird von der alten Android App bzw. bei Android SDK < 11 verwendet.

Er gibt nur drei Qualitäten zurück, diese API ist nicht vollständig verlässlich, sie funktioniert zwar nur für wenige Videos nicht und gibt bei alten Videos nicht die tatsächlich höchste Qualität zurück, aber dennoch sollte auf eine andere Methode zurückgegriffen werden die von der App nicht verwendet wird. Auch ist die Reihenfolge (low->medium->high) der URLs nicht immer richtig.

Es ist keine Authentifizierung erforderlich. Die Header der App sind ebenfalls nicht erforderlich.

Bezüglich Video-ID's siehe den Abschnitt in Metadaten.

### Request
```bash
curl -s -X GET 'https://videos.mtvnn.com/android/videos/fb26b7baa31b90874c885a6d855358e4.json'
```

### Beispielantwort
```json
{
	"low": "http://cdn.riptide-mtvn.com/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_webm_480x272_seg0_480x270_166000.mp4",
	"medium": "http://cdn.riptide-mtvn.com/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_webl_640x360_seg0_640x360_1545000.mp4",
	"high": "http://cdn.riptide-mtvn.com/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_webxl_1280x720_seg0_1280x720_3619000.mp4"
}
```
-----------------------
## GET <video_url> / <iphone_url> (Videos)
Streng genommen kein API Endpunkt, der vollständigkeit halber aber enthalten.

Dieser Request an eine ebenfalls nicht auf gameone.de zu findene Adresse liefert eine m3u8 playlist für einen HLS (HTTP Live Stream) zurück. Dieser wird von der Android App 2.0 ab Android 3.0 und der iOS App verwendet. HLS bietet Adaptives Streaming und ist auf vielen Platformen verfügbar.

Die URL ist als `video_url` bei `tv_show` Objekten und als `iphone_url` in `video_meta` Objekten zu finden.

### Request
```bash
curl -s -X GET 'https://videos.mtvnn.com/fb26b7baa31b90874c885a6d855358e4.m3u8'
```

### Beispielantwort
```text
#EXTM3U
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=3714000,RESOLUTION=1280x720,CODECS="avc1.77.30, mp4a.40.2"
http://hls.mtvnn.com/i/_!/riptide-mtvn/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_,webxl_1280x720_seg0_1280x720_3619000,webl_640x360_seg0_640x360_1545000,webm_480x272_seg0_480x270_166000,.mp4.csmil/index_0_av.m3u8?e=b471643725c47acd
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=1640000,RESOLUTION=640x360,CODECS="avc1.66.30, mp4a.40.2"
http://hls.mtvnn.com/i/_!/riptide-mtvn/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_,webxl_1280x720_seg0_1280x720_3619000,webl_640x360_seg0_640x360_1545000,webm_480x272_seg0_480x270_166000,.mp4.csmil/index_1_av.m3u8?e=b471643725c47acd
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=229000,RESOLUTION=480x270,CODECS="avc1.66.30, mp4a.40.2"
http://hls.mtvnn.com/i/_!/riptide-mtvn/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_,webxl_1280x720_seg0_1280x720_3619000,webl_640x360_seg0_640x360_1545000,webm_480x272_seg0_480x270_166000,.mp4.csmil/index_2_av.m3u8?e=b471643725c47acd
#EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=63000,CODECS="mp4a.40.2"
http://hls.mtvnn.com/i/_!/riptide-mtvn/r2/production/2014/06/27/fb26b7baa31b90874c885a6d855358e4/mp4_,webxl_1280x720_seg0_1280x720_3619000,webl_640x360_seg0_640x360_1545000,webm_480x272_seg0_480x270_166000,.mp4.csmil/index_2_a.m3u8?e=b471643725c47acd
```
-----------------------
# Objekte
## video_meta
Das `video_meta` Objekt wird für Metadatan von Videos verwendet. Hätte man sich denken können, nicht?

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"video_meta": {
		"cached_rating": 0.0, # Bewertung des Videos, nur bei Videos der Playtube verwendet.
		"created_at": "2014-06-27T11:24:07+02:00", # Hochladezeitpunkt
		"description": "Gauntlet Interview", # Beschreibung, ungenutzt
		"featured": false, # Für die Playtube genutzt
		"id": 644065, # ID, nur in der Playtube genutzt
		"midrolls": "", # Werbung, anscheinend ungenutzt
		"riptide_id": null, # Deprecated, für sehr alte Videos genutzt
		"riptide_video_id": "fb26b7baa31b90874c885a6d855358e4", # video_id die auch zum Request verwendet wird
		"title": "Gauntlet Interview", # Titel, außerhalb der iOS App nicht verwendet
		"img_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/644/065/big/640x360.jpg", # Thumbnail
		"iphone_url": "http://videos.mtvnn.com/fb26b7baa31b90874c885a6d855358e4.m3u8", # HLS Playlist URL
		"games_string": "", # Kommaseperierter String, nur in der Playtube verwendet
		"ratings_count": 0, # Anzahl der Bewertungen, nur Playtube
		"total_views": 0, # Anzahl der Aufrufe, nur Playtube
		"duration": 531.2, # Länge in Sekunden (Float)
		"comments_count": 0, # Anzahl der Kommentare
		"small_image_url": "http://s3.gameone.de/gameone/assets/video_metas/teaser_images/000/644/065/medium/640x360.jpg", # kleines Thumbnail
		"tags_string": "", # Kommaseperierte Tags, Playtube...
		"user": {
			"id": 77122, # UserID des Uploaders
			"name": "Bell", # Name des Uploaders, Bell <3
			"avatar_image_url": "*snip*" # Link zum Gravatar des Uploaders
		}
	}
}
```

## audio_meta
Das `audio_meta` Objekt wird für Metadatan von Audiodateien verwendet. Unglaublich, nich wahr?

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"audio_meta": {
		"description": "AppCast #235", # Beschreibung, kann HTML enthalten
		"duration": 0, # Länge in Sekunden (ungenutzt)
		"id": 791, # ID die auch in der Anfrage genutzt wird
		"riptide_id": null, # Deprecated
		"title": "AppCast #235", # Titel
		"iphone_url": "http://s3.gameone.de/gameone/assets/audio_metas/000/000/791/original/AppCast235.mp3", # Link zur Audiodatei
		"user": {
			"id": 205588, # UserID des Uploaders
			"name": "Johannes", # Name des Uploaders
			"avatar_image_url": "*snip*" # Link zum Gravatar des Uploaders
		}
	}
}
```

## gallery
Das `gallery` Objekt wird für Gallerien verwendet. Faszinierend.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"gallery": {
		"active": false, # Falls abstimmbar definiert dies ob die Abstimmung noch aktiv ist
		"description": "Hautnah #300", # Beschreibung
		"ends_at": "2014-10-01T13:43:00+02:00", # Falls abstimmbar definiert dies das Ende der Abstimmphase
		"id": 744, # ID, ungenutzt
		"param": "hautnah300", # ID der Gallerie
		"starts_at": "2014-10-01T13:43:00+02:00", # Falls abstimmbar definiert dies den Beginn der Abstimmphase
		"title": "Hautnah #300", # Titel
		"votable": false, # Bestimmt ob Abstimmbar oder nicht 
		"images": [{ # Array der Bilder
			"cached_rating": 0, # Rating eines Bildes (Falls abstimmbar)
			"caption": "1", # Bildunterschrift
			"position": 1, # Position in der Gallerie
			"image_url": "http://s3.gameone.de/gameone/assets/gallery_pictures/000/018/897/medium/1.jpg" # Link zum Bild (medium für die App)
		},
		{
			...
		}]
	}
}
```