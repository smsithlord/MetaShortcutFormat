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
Everything - games, movies, music, books, links - everything on your PC, & everything on the internet, can be represented as a shortcut.  They are like a roadmap to the data you want.
Your computer goes there & fetches the data for you.  Regular shortcuts look like app icons, text links, or bookmark buttons.  Meta Shortcut Format exists to facilitate a minimalistic rich presence for shortcuts, especially when used in 2D or 3D environments.

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

## Texture Channel Priority
To avoid redundant data values, MSF expects frontends to use a fallback / priority system for generating rich presence for meta shortcuts inside of their 2D/3D environment.  This is especially important when dealing with texture channels.  For example, if a meta shortcut contains **only** the FILE field, then the frontend should automatically attempt to use the FILE value as the screen & marquee textures used on the shortcuts representation in the 2D/3D environment.  That way the best possible rich presence is generated utilizing what ever meta data the shortcut has to offer.

The suggested texture channel priority is as follows:
- **screen texture channel**: (1) screen value, (2) preview value, (3) file value, (4) marquee value
- **marquee texture channel**: (1) marquee value, (2) preview value, (3) file value, (4) screen value

## Suggested In-Game Interactive Preview Priority
Frontends can choose to provide interactive in-game previews for shortcuts if they wish.  If they do this, it is **HIGHLY RECOMMENDED** that they also implement an object select system so that the user can indicate which in-game shortcuts they want to have active interactive previews running on at any given time.  Most shortcuts will be in their inactive state, merely showing their static screen & marquee texture channels on them.  Only the objects that the user is interested in show interactive in-game previews.

You are free to determine what the best in-game interactive preview priority is for your specific frontend.  Below is a general suggestion on what you might want to prioritize:
- **stream** field, if valid.
- **preview** field, if valid.
- **file** field, if valid.
- **screen** field, if valid.
- **marqruee** field, if valid.
- **reference** field, if valid.

Note that you may also want to alter priority based on keywords found in those field values, such as "youtube.com" or "netflix.com".  How you prioritize your in-game interactive previews is entirely up to you.  Do what ever makes sense for your frontend.

## Types
Metaverse types are arbitrary.  Users can create their own "types" and name them what ever they want.  However, here are some standard type names you are likely to encounter:
- 3do, 3ds, 32x, arcade, atari5200, books, cards, comics, ds, gameboy, gamecube, gamegear, gba, gbc, genesis, images, maps, megadrive, movies, music, n64, neogeo, nes, pc, pinball, ps, ps2, ps3, ps4, psp, sms, snes, text, tv, twitch, videos, websites, wii, wiiu, youtube

## Open-With Apps
In standard flat MSF, the **app** field contains the name of a program that is assumed to be required to open the shortcut with.  This is an arbitrary value that is usually absent or just an empty string.  Common values for this field include the names of emulators, such as Project 64 or SNES9x.  In standard flat MSF, this **app** field is merely a hint to the user that they might need additional software to launch the shortcut.  (Note that in the deep variant of MSF, the **app** field is able to play a much more functional role.)

When an **app** field is absent or an empty string, it means the shortcut needs no special handling.  In other words, if you pasted the shortcut target into the Windows Run dialoge, it would open successfully in a native app automatically.

## Tags
Tags are completely arbitrary and used only to provide additional search & filter posibilities to your frontend.

## JSON Examples
```javascript
{"title":"Rogue One: A Star Wars Story (2016)","file":"Rogue One - A Star Wars Story (2016).mp4","screen":"http://image.tmdb.org/t/p/original/tZjVVIYXACV4IIIhXeIM59ytqwS.jpg","marquee":"http://image.tmdb.org/t/p/original/qjiskwlV1qQzRCjpV0cL9pEMF9a.jpg","preview":"https://www.youtube.com/watch?v=wxL8bVJhXCM","reference":"http://www.themoviedb.org/movie/330459","description":"A rogue band of resistance fighters unite for a mission to steal the Death Star plans and bring a new hope to the galaxy.","type":"movies"}
```
```javascript
{"title":"SuperSmashLand","file":"SuperSmashLand.exe","screen":"http://www.supersmashland.com/imgs/screenshot1.png","marquee":"https://i.ytimg.com/vi/KVROb_FPZCc/maxresdefault.jpg","preview":"https://www.youtube.com/watch?v=351CO5_8fbM","download":"http://www.supersmashland.com/","reference":"http://en.wikipedia.org/wiki/Super_Smash_Land","description":"Super Smash Land is a demake of Super Smash Bros. released in September 14, 2011 by Dan Fornace. The game features 6 playable characters and 11 stages. The game visual design resembles the graphics from the Nintendo Game Boy. The game was developed with GameMaker 7.","keywords":"retro, nintendo","type":"pc"}
```
```javascript
{"title":"Antz (1998)","file":"Antz (1998).avi","screen":"http://cf2.imgobject.com/t/p/original/qvHnMakgkH6UK8nUCaQYb8dlGSq.jpg","marquee":"http://cf2.imgobject.com/t/p/original/zoUwYRJSwatBBvBDRf1y0RtiytI.jpg","preview":"http://www.youtube.com/watch?v=6kqGO1c70ak","stream":"http://www.netflix.com/watch/17236549","reference":"http://www.themoviedb.org/movie/8916","description":"In this animated hit, a neurotic worker ant in love with a rebellious princess rises to unlikely stardom when he switches places with a soldier. Signing up to march in a parade, he ends up under the command of a bloodthirsty general. But he's actually been enlisted to fight against a termite army.","keywords":"animals, insects, animated","type":"movies"}
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

## Frontend Design
If your frontend will manage multiple MSF items at the same time, it is recommended that you assign an ID to each MSF item and store them in a library.  That way objects in your frontend just need to reference an item ID in order to know which meta data is assigned to them.

Note that, in the **deep variant of MSF**, an item ID is **included** for you in the shortcut's meta data.

The suggested way to store your items in a library object is as follows (replacing *ITEM_ID* with the ID you assign to the item and *ITEM_DATA_OBJECT* with the actual meta data for the item):
```javascript
var library = {
  items:
  {
    ITEM_ID: ITEM_DATA_OBJECT,
    ITEM_ID: ITEM_DATA_OBJECT,
    ITEM_ID: ITEM_DATA_OBJECT,
    ITEM_ID: ITEM_DATA_OBJECT,
    ITEM_ID: ITEM_DATA_OBJECT
  }
};
```

## Texture Image Caching
It is recommended that your frontend cache textures between sessions, especially textures that are generated from web URLs.  This will drastically reduce the amount of network calls your frontend needs to make and also insures that the shortcut looks right even if the user's internet dies or the original image source no longer exists.
