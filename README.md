#Meta Shortcut Format
----------------------------------------------------
Title: (string) the name of the shortcut
File: (string) the file target of the shortcut
Screen: (string) the image to use on the shortut's screen
Marquee: (string) the image to use on the shortcut's marquee
Preview: (string) an addition file target to show as a preview
Reference: (string) a URL to an arbitrary online database entry related to this shortcut
Stream: (string) a URL to stream the shortcut
Download: (string) a URL to download the shortcut
Description: (string) a description of the shortcut
Tags: (string) comma separated list of keywords
Open With: (string) the name of an app that is used to open this shortcut.
Type: (string) the name of a type associated with this shortcut.
----------------------------------------------------

Preface:
The purpose of this specification is so other frontends can support the type of META SHORTCUTS seen in Anarchy Arcade.  By treating shortcuts as distinct objects with fields as specified in this document, any capable 3D or 2D engine can add perfect metaverse browser functionality.

Purpose:
The Meta Shortcut Format (MSF) was developed out of necessity over the past 10 years by myself (SM Sith Lord) based heavily on feedback from users of my 3D metaverse browser Anarchy Arcade.

A meta shortcut is very much like a regular desktop shortcut, but with a few extra fileds that (1) make it suitable to represent mixed web/local shortcuts, (2) make it far more capable of generating a rich presence for itself within a 2D or 3D environment, and (3) provide enough meta data for shortcuts to be used in a mutliplayer environment effectively.

Scope:
Meta shortcuts hold plain-text meta data only.  No binary data.  The only required field is FILE.  The other fields may be left blank.  The amount of meta data present in a shortcut will determine how well its rich presence will be in the interactive 2D or 3D environment.

Encoding:
The MSF can be encoded by any appropriate method (JSON, XML, etc.) as long as the meta data is retained.  The most basic MSF is flat & contains only plain-text string fields.  Note that there is also a deep variant that provides extended support for the OPEN WITH and TYPE fields as well as a way to specify what kind of 3D model the shortcut would like to be displayed on, but the specification in this document is for the standard flat variant only.

Values:
All feild values are strings.  Frontends should support at least 1024 characters in each field, but may support much more if they wish.  The following fields expect plain-text: Title, Description, Tags, Type, Open With.  Conversly, the other fields expect either a local file target or a URL: File, Screen, Marquee, Preview, Stream, Download, Reference.

Security & Privacy:
When a user shares a meta shortcut that has references to local files in its meta data, it is common practice to conceal the user's local folder structure by removing all but the file name from the field's value.
