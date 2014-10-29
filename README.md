Yosemite System Font Patcher
============================

Change the system font of Mac OS X Yosemite.
Inspired by [FiraSystemFontReplacement](https://github.com/jenskutilek/FiraSystemFontReplacement).

Maybe it's just me, but for such a new and modern interface, Helvetica Neue feels… _ancient_,
and Helvetica is already everywhere…
A more futuristic font such as Avenir Next may be a better choice.

<img src="http://i.imgur.com/I84LhWq.png" width="444.5" height="414.5" alt="Replacing the system font with Avenir next">


New: Step by Step Tutorial
--------------------------

<br>

[![Step by Step Tutorial](https://svg-buttons.herokuapp.com/button/plain.svg?button_width=440&text=Step+By+Step+Tutorial)](https://github.com/dtinth/YosemiteSystemFontPatcher/wiki/Step-by-Step-Guide)

<br>

Prerequisites
-------------

First, install [Homebrew](http://brew.sh/). Then install FontForge with Python support.

```bash
brew install fontforge --with-python
```

Make sure FontForge works in Python:

```python
python -c 'import fontforge; print "FontForge works in Python"'
```


New: Convenient Script
----------------------

A convenient script is provided for you to convert fonts using a GUI wizard. In your Terminal, `cd` to the project folder and run:

```bash
bin/convenient-script
```


Patching a Font (Manual)
---------------

Copy __HelveticaNeueDeskInterface.ttc__ from __/System/Library/Fonts/__ to the root of the repository. Then run the following command:

```bash
bin/patch 'System Font Name' 'Font To Use'
```

Where `System Font Name` is\*:

| System Font Name\* | Description | &nbsp; |
| ---------------- | ----------- | ------ |
| System Font Regular | Regular | :star: |
| System Font Bold | Bold | :star: |
| System Font Italic | Italic | &nbsp; |
| System Font Bold Italic | Bold | &nbsp; |
| System Font Medium P4 | Medium - used in notification title | :star: |
| System Font Medium Italic P4 | Medium Italic | &nbsp; |
| システムフォント レギュラ ライト | Light | &nbsp; |
| System Font Thin | Thin | &nbsp; |
| System Font UltraLight | Ultra Light | &nbsp; |
| System Font Heavy | Heavy | &nbsp; |

(\* note: the above table is for English locale. For other locales, you must check the list of system font names by running `bin/list-fonts HelveticaNeueDeskInterface.ttc` — see issue [#1](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/1))

...and `Font To Use` is the path to the font file you want to use.
For example, `Raleway-Medium.ttf`.

Some fonts come in `.ttc` file format, which contains many fonts in one file. For instructions to use them, see below.

The font names that I did not put a star on are rarely used; you don't have to patch it.

The script will

* open the font file to use,
* scale and adjust the metrics to match that of the system font (that's why the script needs `HelveticaNeueDeskInterface.ttc` to be present),
* adjust the PostScript name to match with the system font, and
* save the font into current directory.


### Specifying a `.ttc` File

A `.ttc` file contains several fonts in one file.
Most fonts that comes with OS X come in this format.
To select a font inside `.ttc` file, [put the font name inside the parentheses](http://fontforge.org/cliargs.html).
For example, `Avenir Next.ttc(Avenir Next Medium)`.


Installation
------------

Simply copy the generated font files to `~/Library/Fonts`.
Mac OS X will use these fonts instead of the system fonts.


Example
-------

To make __Avenir Next__ your system font, copy __Avenir Next.ttc__ from __/Library/Fonts__ into the repository root, and then use this script:

```bash
#!/bin/bash -e
bin/patch 'System Font Regular'            'Avenir Next.ttc(Avenir Next Medium)'
bin/patch 'System Font Bold'               'Avenir Next.ttc(Avenir Next Bold)'
bin/patch 'System Font Italic'             'Avenir Next.ttc(Avenir Next Medium Italic)'
bin/patch 'System Font Bold Italic'        'Avenir Next.ttc(Avenir Next Bold Italic)'
bin/patch 'System Font Medium P4'          'Avenir Next.ttc(Avenir Next Demi Bold)'
bin/patch 'System Font Medium Italic P4'   'Avenir Next.ttc(Avenir Next Demi Bold Italic)'
```

It generates:

- System Avenir Next Bold Italic.ttf
- System Avenir Next Bold.ttf
- System Avenir Next Demi Bold Italic.ttf
- System Avenir Next Demi Bold.ttf
- System Avenir Next Medium Italic.ttf
- System Avenir Next Medium.ttf


Now you can copy these files into `~/Library/Fonts`, log out, and log back in. You should see the font changed!

Thanks
------

I consulted these resources in creating the script:

- [jenskutilek/FiraSystemFontReplacement](https://github.com/jenskutilek/FiraSystemFontReplacement)
- [Lokaltog/powerline-fontpatcher](https://github.com/Lokaltog/powerline-fontpatcher)
- [Design With FontForge: Line Spacing](http://designwithfontforge.com/en-US/Line_Spacing.html)
- [Writing python scripts to change fonts in FontForge](http://fontforge.org/python.html)
- [kawabata/hanamin-kdp - makefont.py](https://github.com/kawabata/hanamin-kdp/blob/master/makefont.py)
