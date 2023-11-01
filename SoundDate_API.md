# SoundDate API

## `POST profile/sound`

Uploads a sound file to the user's profile.

`POST https://api.sounddate.com/profile/sound`

### Headers

Header | Description | Required | Notes
-------|-------------|----------|------
`Bearer` | The access token. | Required | See authorization section.
`Content-Type` | The format of the sound file to send. | Optional | Acceptable values: `audio/mpeg` for MP3 files or `audio/x-wav` for wav files. Default value: `audio/mpeg`.
`Accept` | The format of the response. | Optional | Acceptable values: `application/xml` or `application/json`. Default value: `application/json`.

### POST body

The sound file, which must be 5 minutes or less.

### Sample request

```
POST https://api.sounddate.com/profile/sound

Bearer: YOUR_ACCESS_TOKEN
Content-Type: audio/mpeg
Accept: application/json

{
  The sound file
}
```

### Response

Element | Description | Type | Notes
--------|-------------|------|------
`id` | The ID of the new sound file. | Integer
`length` | The length of the sound file. | Float | In seconds


### Sample response

```
{
  "id": "12345"
  "length": "150.5
}
```

## `GET /user/{user id}/profile/sound`

Retrieves the user's sound files.

`GET https://api.sounddate.com/user/{user id}/profile/sound`

### Path parameters

Parameter | Description | Type | Required | Notes
----------|-------------|------|----------|------
`user id` | The user's ID. | Integer | Required

### Query parameters

Parameter | Description | Type | Required | Notes
----------|-------------|------|----------|------
`sortOrder` | The order in which the sound files are returned. | String | Optional | Acceptable values: `mostRecent`: Sorts most recent to earliest; `earliest`: Sorts earliest to most recent; `shortest`: Shorts shortest to longest; `longest`: Sorts longest to shortest. Default value: `mostRecent`

### Headers

Header | Description | Required | Notes
-------|-------------|----------|------
`Bearer` | The access token. | Required
`Accept` | The format of the response. | Optional | Acceptable values: `application/xml` or `application/json`. Default value: `application/json`.

### Sample request

```
GET https://api.sounddate.com/user/345354/profile/sound?sortOrder=shortest

Bearer: ACCESS_TOKEN
Accept: application/json
```

### Response

Element | Description | Type | Notes
--------|-------------|------|------
`soundFiles` | The parent object that contains the sound files. | Array
`id` | The ID of the sound file. | Integer
`url` | The URL of the sound file. | String
`length` | The length of the sound file. | Float | In seconds.

```
Sample response
{
  "soundFiles": [
    {
      "id": 23456,
      "url": "https://api.sounddate.com/profile/sound/23456.mp3",
      "length": 11.2
    },
    {
      "id": 24559,
      "url": "https://api.sounddate.com/profile/sound/24559.mp3",
      "Length": 19.8
    }
  ]
}
```

### Status codes and errors

Code | Description | Notes
-----|-------------|------
`200` | Success | Sound file retrieved or created.
`401` | Unauthorized | Invalid access token.
`413` | Payload too large | Sound file longer than 5 minutes.

