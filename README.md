# Meta Shortcut Format

- **title**: (string) the name of the shortcut
- **file**: (string) the file target of the shortcut
- **screen**: (string) the image to use on the shortut's screen
- **marquee**: (string) the image to use on the shortcut's marquee
- **preview**: (string) an addition file target to show as a preview
- **reference**: (string) a URL to an arbitrary online database entry related to this shortcut
- **stream**: (string) a URL to stream the shortcut
- **download**: (string) a URL to download the shortcut
- **description**: (string) a description of the shortcut
- **tags**: (string) comma separated list of keywords
- **app**: (string) the name of an app that is used to open this shortcut
- **type**: (string) the name of a type associated with this shortcut.

## Preface
The purpose of this specification is so other frontends can support the type of **META SHORTCUTS** seen in Anarchy Arcade.  By treating shortcuts as distinct objects with fields as specified in this document, any capable 3D or 2D engine can add perfect metaverse browser functionality.

## Purpose
The Meta Shortcut Format (MSF) was developed out of necessity over the past 10 years by myself (SM Sith Lord) based heavily on feedback from users of my 3D metaverse browser Anarchy Arcade.

A meta shortcut is very much like a regular desktop shortcut, but with a few extra fileds that **(1)** make it suitable to represent mixed web/local shortcuts, **(2)** make it far more capable of generating a rich presence for itself within a 2D or 3D environment, and **(3)** provide enough meta data for shortcuts to be used in a mutliplayer environment effectively.

Meta shorcuts are engine agnostic.  They are purely a way to represent shortcut meta data.

## Scope
Meta shortcuts hold plain-text meta data only.  No binary data.  The only required field is FILE.  The other fields may be left blank.  The amount of meta data present in a shortcut will determine how well its rich presence will be in the interactive 2D or 3D environment.

## Encoding
The MSF can be encoded by any appropriate method (JSON, XML, etc.) as long as the meta data is retained.  The most basic MSF is flat & contains only plain-text string fields.  Note that there is also a deep variant that provides extended support for the OPEN WITH and TYPE fields as well as a way to specify what kind of 3D model the shortcut would like to be displayed on, but the specification in this document is for the standard flat variant only.

## Values
All feild values are strings.  Frontends should support at least 1024 characters in each field, but may support much more if they wish.  The following fields expect plain-text: Title, Description, Tags, Type, Open With.  Conversly, the other fields expect either a local file target or a URL: File, Screen, Marquee, Preview, Stream, Download, Reference.  If a particular field does not exist in a shortcut, it is assumed to be the default value of an empty string.

## Security & Privacy
When a user shares a meta shortcut that has references to local files in its meta data, it is common practice to conceal the user's local folder structure by removing all but the file name from the field's value.

## Types
Metaverse types are arbitrary.  Users can create their own "types" and name them what ever they want.  However, here are some standard type names you are likely to encounter:
- 3do, 3ds, 32x, arcade, atari5200, books, cards, comics, ds, gameboy, gamecube, gamegear, gba, gbc, genesis, images, maps, megadrive, movies, music, n64, neogeo, nes, pc, pinball, ps, ps2, ps3, ps4, psp, sms, snes, text, tv, twitch, videos, websites, wii, wiiu, youtube

## JSON Examples
```javascript
{"title":"Rogue One: A Star Wars Story (2016)","file":"Rogue One - A Star Wars Story (2016).mp4","screen":"http://image.tmdb.org/t/p/original/tZjVVIYXACV4IIIhXeIM59ytqwS.jpg","marquee":"http://image.tmdb.org/t/p/original/qjiskwlV1qQzRCjpV0cL9pEMF9a.jpg","preview":"https://www.youtube.com/watch?v=wxL8bVJhXCM","reference":"http://www.themoviedb.org/movie/330459","description":"A rogue band of resistance fighters unite for a mission to steal the Death Star plans and bring a new hope to the galaxy.","type":"movies"}
```
```javascript
{"title":"SuperSmashLand","file":"SuperSmashLand.exe","screen":"http://www.supersmashland.com/imgs/screenshot1.png","marquee":"https://i.ytimg.com/vi/KVROb_FPZCc/maxresdefault.jpg","preview":"https://www.youtube.com/watch?v=351CO5_8fbM"}
```
```javascript
{"title":"Look Who's Talking (1989)","file":"Look Who's Talking (1989)","screen":"http://image.tmdb.org/t/p/original/m9TyWTTaaFUNMlNJ3b8Q0gkOiZY.jpg","marquee":"http://image.tmdb.org/t/p/original/zyq8wUKk3FVfgkYnI1IVgmypOtG.jpg","preview":"http://www.youtube.com/watch?v=yOB_MqcaZHw","reference":"http://www.themoviedb.org/movie/9494","description":"Mollie is a single working mother who's out to find the perfect father for her child. Her baby, Mikey, prefers James, a cab driver turned babysitter who has what it takes to make them both happy. But Mollie won't even consider James. It's going to take all the tricks a baby can think of to bring them together before it's too late","type":"movies"}
```
```javascript
{"title":"Neon Drive","file":"steam://run/433910","screen":"http://cdn.steamstatic.com/steam/apps/433910/header.jpg","marquee":"http://cdn.steamstatic.com/steam/apps/433910/header.jpg","preview":"http://www.youtube.com/watch?v=UTkioWWjpsw","reference":"http://store.steampowered.com/app/433910","type":"pc"}
```
```javascript
{"title":"Star Trek: Deep Space Nine on Netflix","file":"https://www.netflix.com/title/70158330","screen":"https://wallpapercave.com/wp/pBL9PTN.jpg","type":"tv"}
```
```javascript
{"title":"▶ Botnit - Hi-Score","file":"https://www.youtube.com/watch?v=8wDrUPlo15M","screen":"http://img.youtube.com/vi/8wDrUPlo15M/0.jpg","description":"Reupload of the classic Maniac Synth video","type":"youtube"}
```
```javascript
{"title":"The Simpsons","file":"https://www.hulu.com/the-simpsons","screen":"http://a248.e.akamai.net/ib.huluim.com/show_key_art/58?size=1280x720","marquee":"http://assetshuluimcom-a.akamaihd.net/h2o/facebook_share_thumb_default_hulu.png","stream":"https://www.hulu.com/the-simpsons","description":"Watch The Simpsons online. Stream episodes and clips of The Simpsons instantly.","type":"tv"}
```
```javascript
{"title":"Purple Trees","file":"https://kosmetista.ru/uploads/images/07/04/95/2015/06/11/82c72c.jpg","type":"images"}
```
