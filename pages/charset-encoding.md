## Characters and Encoding
* `Character` - is the smallest *element of meaning*. It can be letter, spacing character, symbol or even a word. 
Examples: A B | + $ etc.

* `Character Set` (or `charset`) - is a *collection* of that characters (sometimes mistakenly synonymous with *Code Page*; they are related but not the same). Each Character in the collection has a *Code Point* or a unique number. One charset might be used by multiple languages. For example, latin letters are used in various European languages. In general, most of charsets are formed naturally and united under some category. As a rule, charsets are collections without a method of *Encoding* them (or representing in machine readable form).
Examples: Unicode (UCS), language alphabets, greek numbers, etc.

* `Encoding` -  it is *how* a mapping between Character Set and machine readable form of its Characters is done. Often used interchangeably with the Code Page term (which is good way to go). However, Encoding has more general sense and might include the latter. Examples fit to both Encodings and Code Pages: UTF-8/16, ASCII, KOI8, ISO 8859 (Latin-1), Windows-1252 (CP-1252), CP437, etc. 

* `Code Page` (or `coded character sets`) - is a *table* where each Character has been assigned a *unique* number. Code Pages could contain multiple charsets imposed on the same table with one method of Encoding. Think of Code Pages being a conventional table of Characters mapped to (human readable) numbers and Encodings being a program technique of how that Characters must be encoded to (machine readable) byte form. 

* `Code Point` - is a *unique number* assigned to a Character that makes up a *Code Space* of Character Set.

* `Glyph` - is a *graphical representation* of a Character. Character can be one but has several glyphs. Examples: Α, *Α*, **Α**.

```
[            256-65536] - ISO 10646, UCS, Universal Character Set or just Unicode (16/32bit)
[     128-255]          - ISO 8859-1, CP-1252, KOI8 (8bit)
[0-127]                 - US-ASCII or just "classic" ASCII (7bit)
First 0-65536(0xFFFF) code points of Unicode are "basic multilingual plane" (BMP), all other are "supplementary characters"
```

References:
1. https://blogs.msdn.microsoft.com/shawnste/2005/03/15/whats-the-difference-between-an-encoding-code-page-character-set-and-unicode/
1. https://en.wikipedia.org/wiki/Character_encoding#Terminology
1. https://stackoverflow.com/questions/3441490/whats-the-difference-between-an-encoding-a-character-set-and-a-code-page

#### Programs
* `iconv`

#### Files
