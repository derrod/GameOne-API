# Login, Sessions und User

Die API Funktionen zum einloggen und abrufen von informationen über die aktuelle session und User.

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

# API-Endpoints
## POST /session.json
Dieser Endpoint kann bei verwendung des Authorization Headers außer zum einmaligen prüfen des Logins missachtet werden.
### Parameter

| Name | Erforderlich | Typ | Beschreibung |
| ---- | ------------ | --- | ------------ |
| `user_session[user_login]` | Ja | String | Username der zum einloggen verwendet werden soll |
| `user_session[password]` | Ja | String | Passwort für den verwendeten Usernamen |


### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -F 'user_session[password]=<password>' -F 'user_session[user_login]=test_user2' -X POST 'https://gameone.de/session.json'
```
### Response (mit 1UP Subscription)
```json
{
  "user": {
    "active": true,
    "id": 12345,
    "subscription": 1,
    "subscription_end_date": "2014-10-14T23:09:37+02:00",
    "user_login": "test_user1",
    "user_registered": "2011-11-09T22:21:53+01:00",
    "name": "test_user1",
    "avatar_image_url": "http://www.gravatar.com/avatar/c91e49ed70279487c9c485a156b0664e?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png",
    "user_stats": {
      "pinboard": 0,
      "posts": 40,
      "comments": 53,
      "playtube": 5
    }
  }
}
```

### Response (ohne 1UP Subscription)
```json
{
  "user": {
    "active": true,
    "id": 123456,
    "subscription": 0,
    "subscription_end_date": "2013-02-14T18:11:57+01:00",
    "user_login": "test_user2",
    "user_registered": "2012-10-12T18:50:18+02:00",
    "name": "test_user2",
    "avatar_image_url": "http://www.gravatar.com/avatar/c91e49ed70279487c9c485a156b0664e?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png",
    "user_stats": {
      "pinboard": 0,
      "posts": 0,
      "comments": 1,
      "playtube": 0
    }
  }
}
```
### Response (Errors / Fehlermeldungen)
Ungültiger username:

`HTTP/1.1 401 Unauthorized` und
```json
{
  "errors": [
    "User login ist falsch"
  ]
}
```
Falsches Passwort:

`HTTP/1.1 401 Unauthorized` und
```json
{
  "errors": [
    "Passwort ist falsch"
  ]
}
```
-----------------------
## GET /users/me.json
Erfordert Autorisierung (Cookie oder Authorization Header), keine Parameter.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -H 'Authorization: Basic <auth>' -X GET 'https://gameone.de/users/me.json'
```
### Response (mit 1UP Subscription)
```json
{
  "user": {
    "active": true,
    "id": 12345,
    "subscription": 1,
    "subscription_end_date": "2014-10-14T23:09:37+02:00",
    "subscription_type": "AUTORENEWING",
    "user_login": "test_user1",
    "user_registered": "2011-11-09T22:21:53+01:00",
    "name": "test_user1",
    "avatar_image_url": "http://www.gravatar.com/avatar/c91e49ed70279487c9c485a156b0664e?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png",
    "user_stats": {
      "pinboard": 0,
      "posts": 40,
      "comments": 53,
      "playtube": 5
    },
    "subscriptions": [
      {
        "product_identifier": "de.gameone.iphone.powerup.month",
        "type": "AUTORENEWING",
        "end_date": "2014-10-14T23:09:37+02:00",
        "days_left": 20
      }
    ]
  }
}
```
### Response (ohne 1UP Subscription)
```json
{
  "user": {
    "active": true,
    "id": 123456,
    "subscription": 0,
    "subscription_end_date": "2013-02-14T18:11:57+01:00",
    "subscription_type": "NONRENEWING",
    "user_login": "test_user2",
    "user_registered": "2012-10-12T18:50:18+02:00",
    "name": "test_user2",
    "avatar_image_url": "http://www.gravatar.com/avatar/c91e49ed70279487c9c485a156b0664e?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png",
    "user_stats": {
      "pinboard": 0,
      "posts": 0,
      "comments": 1,
      "playtube": 0
    },
    "subscriptions": []
  }
}
```
-----------------------
## GET /users/<id>.json
Erfordert Autorisierung (Cookie oder Authorization Header), keine Parameter.

### Request
```bash
curl -s -H 'X-G1APP-IDENTIFIER: x' -A 'GameOne' -H 'Authorization: Basic <auth>' -X GET 'https://gameone.de/users/77122.json'
```
### Response (mit 1UP Subscription)
```json
{
	"user": {
		"id": 77122,
		"user_login": "Bell",
		"user_registered": "2010-07-01T15:54:50+02:00",
		"name": "Bell",
		"avatar_image_url": "http://www.gravatar.com/avatar/6c9192e4d5959783b254941aa8d8e9a7?rating=PG&size=100&default=http%3A%2F%2Fassets.gameone.de%2Fimages%2Fdummys%2Fgravatar2x.png",
		"user_stats": {
			"pinboard": 151,
			"posts": 224,
			"comments": 159,
			"playtube": 14
		}
	}
}
```

-----------------------
# Objektbeschreibungen
## user (login)
Dieses `user` Objekt bekommt man beim erfolgreichen Login zugesendet.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
  "user": {
    "active": true, # Angabe ob der Account aktiv ist oder nicht (gebannt?)
    "id": 12345, # ID des Users
    "subscription": 1, # 1 oder 0 je nachdem ob ein 1UP Abonnement vorhanden ist
    "subscription_end_date": "2014-10-14T23:09:37+02:00", # Enddatum eines Abonnements, bei einem Account der nie ein Abo besaß vermutlich leer
    "user_login": "test_user1", # Loginname
    "user_registered": "2011-11-09T22:21:53+01:00", # Registrierungsdatum
    "name": "test_user1", # Anzeigename des Users
    "avatar_image_url": "*snip*", # Gravatar des Users
    "user_stats": { # Statistiken, selbsterklärend
      "pinboard": 0, # Anzahl der Einträge auf der Pinnwand des Users
      "posts": 40, # Posts im Forum
      "comments": 53, # Kommentare unter Videos/Posts
      "playtube": 5 # Videos auf der Playtube
    }
  }
}
```

## user (me)
Dieses `user` Objekt bekommt man bei einer `GET /users/me.json` Anfrage zugesendet.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
  "user": {
    "active": true, # Angabe ob der Account aktiv ist oder nicht (gebannt?)
    "id": 12345, # ID des Users
    "subscription": 1, # 1 oder 0 je nachdem ob ein 1UP Abonnement vorhanden ist
    "subscription_end_date": "2014-10-14T23:09:37+02:00", # Enddatum eines Abonnements, bei einem Account der nie ein Abo besaß vermutlich leer
    "subscription_type": "AUTORENEWING", # Typ des Abonnements, "AUTORENEWING" oder "NONRENEWING" sind bekannt, evtl. andere Werte möglich
    "user_login": "test_user1", # Loginname
    "user_registered": "2011-11-09T22:21:53+01:00", # Registrierungsdatum
    "name": "test_user1", # Anzeigename des Users
    "avatar_image_url": "*snip*", # Gravatar des Users
    "user_stats": { # Statistiken, selbsterklärend
      "pinboard": 0, # Anzahl der Einträge auf der Pinnwand des Users
      "posts": 40, # Posts im Forum
      "comments": 53, # Kommentare unter Videos/Posts
      "playtube": 5 # Videos auf der Playtube
    },
    "subscriptions": [ # Informationen des Abonnements, wenn keine vorhanden ist ein leeres Array s.o.
      {
        "product_identifier": "de.gameone.iphone.powerup.month", # Identifier des Abos, erkennbar ob unter iOS oder Android abgeschlossen sowie länge
        "type": "AUTORENEWING", # Nochmals Typ, s.o.
        "end_date": "2014-10-14T23:09:37+02:00", # Enddatum
        "days_left": 20 # Anzahl der Verbleibenden Tage
      }
    ]
  }
}
```

## user (anderer)
Dieses `user` Objekt bekommt man bei der Anfrage nach den Informationen eines anderen Users zugesendet.

In diesem Abschnitt werden die Bedeutungen der einzelnen Keys (soweit bekannt) genannt:
```bash
{
	"user": {
		"id": 77122, # ID des Users
		"user_login": "Bell", # Loginname
		"user_registered": "2010-07-01T15:54:50+02:00", # Registrierungsdatum
		"name": "Bell", # Anzeigename des Users
		"avatar_image_url": "*snip*", # Gravatar des Users
		"user_stats": { # Statistiken, selbsterklärend
			"pinboard": 151, # Anzahl der Einträge auf der Pinnwand des Users
			"posts": 224, # Posts im Forum
			"comments": 159, # Kommentare unter Videos/Posts
			"playtube": 14 # Videos auf der Playtube
		}
	}
}
```
