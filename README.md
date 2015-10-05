Yosemite and El Capitan System Font Patcher
===========================================

Change the system font of Mac OS X Yosemite and El Capitan.
Inspired by [FiraSystemFontReplacement](https://github.com/jenskutilek/FiraSystemFontReplacement).

Maybe it's just me, but for such a new and modern interface, Helvetica Neue feels… _ancient_,
and Helvetica is already everywhere…
A more futuristic font such as Avenir Next may be a better choice.

<img src="http://i.imgur.com/I84LhWq.png" width="444.5" height="414.5" alt="Replacing the system font with Avenir next">


Project Status: Help Wanted
-------------------------------

The software provided here works for me, and I get the Avenir Next font I wanted.
You can also use this software to patch fonts for your own use as well.
However, there are few minor issues, such as [font baseline issue](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/12).
I'd like some help from the community to resolve these, especially font experts.


New: Step by Step Tutorial (Yosemite Only)
------------------------------------------

<br>

<p align="center">
<strong>Note:</strong>
The convenient script and step by step tutorial currently only works for Yosemite.
Contributions to help update this to also work with El Capitan would be much appreciated.
</p>

[![Step by Step Tutorial](https://svg-buttons.herokuapp.com/button/plain.svg?button_width=440&text=Step+By+Step+Tutorial)](https://github.com/dtinth/YosemiteSystemFontPatcher/wiki/Step-by-Step-Guide)

<br>

Prerequisites
-------------

### Using Homebrew (easy!)

__Note:__ [This method doesn't seem to work anymore on Yosemite 10.10.3](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/18#issuecomment-111650844). You can try [installing using MacPorts](#using-macports-for-those-who-prefer) (see [the discussion](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/18#issuecomment-111650844)) or if you don't like MacPorts, try [running YosemiteSystemFontPatcher inside a Linux box](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/17#issuecomment-111446387).

First, install [Homebrew](http://brew.sh/) and [XQuartz](https://xquartz.macosforge.org/landing/). Then install FontForge with Python support.

```bash
brew install fontforge --with-python
```

Make sure FontForge works in Python:

```python
python -c 'import fontforge; print "FontForge works in Python"'
```


### Using MacPorts (for those who prefer)

[Instructions provided by @AluminumPea.](https://github.com/dtinth/YosemiteSystemFontPatcher/issues/18#issuecomment-111650844) After installing MacPorts, install Fontforge with Python 2.7 support and switch to that Python. Make sure that you are not using Homebrew's Python!

```bash
sudo port install fontforge +python27
sudo port select --set python python27
```


New: Convenient Script (Yosemite Only)
--------------------------------------

<p align="center">
<strong>Note:</strong>
The convenient script and step by step tutorial currently only works for Yosemite.
Contributions to help update this to also work with El Capitan would be much appreciated.
</p>

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

Simply copy the generated font files to `/Library/Fonts`.
Mac OS X will use these fonts instead of the system fonts.


Examples
--------

### El Capitan

The following Bash script converts Avenir Next into a system font usable with El Capitan.

```sh
patch-system-font() {
  BASE="$1"
  REPLACEMENT="$2"
  ./bin/patch "/System/Library/Fonts/$BASE" "/System/Library/Fonts/$REPLACEMENT"
}

patch-system-font 'SFNSDisplay-Black.otf' 'Avenir Next.ttc(Avenir Next Heavy)'
patch-system-font 'SFNSDisplay-Bold.otf' 'Avenir Next.ttc(Avenir Next Bold)'
patch-system-font 'SFNSDisplay-Heavy.otf' 'Avenir Next.ttc(Avenir Next Heavy)'
patch-system-font 'SFNSDisplay-Light.otf' 'Avenir Next.ttc(Avenir Next Regular)'
patch-system-font 'SFNSDisplay-Medium.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSDisplay-Regular.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSDisplay-Semibold.otf' 'Avenir Next.ttc(Avenir Next Demi Bold)'
patch-system-font 'SFNSDisplay-Thin.otf' 'Avenir Next.ttc(AvenirNext-UltraLight)'
patch-system-font 'SFNSDisplay-Ultralight.otf' 'Avenir Next.ttc(AvenirNext-UltraLight)'
patch-system-font 'SFNSText-Bold.otf' 'Avenir Next.ttc(Avenir Next Bold)'
patch-system-font 'SFNSText-BoldG1.otf' 'Avenir Next.ttc(Avenir Next Bold)'
patch-system-font 'SFNSText-BoldG2.otf' 'Avenir Next.ttc(Avenir Next Bold)'
patch-system-font 'SFNSText-BoldG3.otf' 'Avenir Next.ttc(Avenir Next Bold)'
patch-system-font 'SFNSText-BoldItalic.otf' 'Avenir Next.ttc(Avenir Next Bold Italic)'
patch-system-font 'SFNSText-BoldItalicG1.otf' 'Avenir Next.ttc(Avenir Next Bold Italic)'
patch-system-font 'SFNSText-BoldItalicG2.otf' 'Avenir Next.ttc(Avenir Next Bold Italic)'
patch-system-font 'SFNSText-BoldItalicG3.otf' 'Avenir Next.ttc(Avenir Next Bold Italic)'
patch-system-font 'SFNSText-Heavy.otf' 'Avenir Next.ttc(Avenir Next Heavy)'
patch-system-font 'SFNSText-HeavyItalic.otf' 'Avenir Next.ttc(Avenir Next Heavy Italic)'
patch-system-font 'SFNSText-Light.otf' 'Avenir Next.ttc(Avenir Next Regular)'
patch-system-font 'SFNSText-LightItalic.otf' 'Avenir Next.ttc(Avenir Next Italic)'
patch-system-font 'SFNSText-Medium.otf' 'Avenir Next.ttc(Avenir Next Demi Bold)'
patch-system-font 'SFNSText-MediumItalic.otf' 'Avenir Next.ttc(Avenir Next Demi Bold Italic)'
patch-system-font 'SFNSText-Regular.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSText-RegularG1.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSText-RegularG2.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSText-RegularG3.otf' 'Avenir Next.ttc(Avenir Next Medium)'
patch-system-font 'SFNSText-RegularItalic.otf' 'Avenir Next.ttc(Avenir Next Medium Italic)'
patch-system-font 'SFNSText-RegularItalicG1.otf' 'Avenir Next.ttc(Avenir Next Medium Italic)'
patch-system-font 'SFNSText-RegularItalicG2.otf' 'Avenir Next.ttc(Avenir Next Medium Italic)'
patch-system-font 'SFNSText-RegularItalicG3.otf' 'Avenir Next.ttc(Avenir Next Medium Italic)'
patch-system-font 'SFNSText-Semibold.otf' 'Avenir Next.ttc(Avenir Next Demi Bold)'
patch-system-font 'SFNSText-SemiboldItalic.otf' 'Avenir Next.ttc(Avenir Next Demi Bold Italic)'
```

After running this script, copy the resulting font files to `/Library/Fonts`.


### Yosemite

To make __Avenir Next__ your system font, copy __Avenir Next.ttc__ from __/System/Library/Fonts__ into the repository root, and then use this script:

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


Now you can copy these files into `/Library/Fonts`, log out, and log back in. You should see the font changed!

Thanks
------

I consulted these resources in creating the script:

- [jenskutilek/FiraSystemFontReplacement](https://github.com/jenskutilek/FiraSystemFontReplacement)
- [Lokaltog/powerline-fontpatcher](https://github.com/Lokaltog/powerline-fontpatcher)
- [Design With FontForge: Line Spacing](http://designwithfontforge.com/en-US/Line_Spacing.html)
- [Writing python scripts to change fonts in FontForge](http://fontforge.org/python.html)
- [kawabata/hanamin-kdp - makefont.py](https://github.com/kawabata/hanamin-kdp/blob/master/makefont.py)


Disclaimer
----------

- This software has been provided AS-IS. Use at your own risk.
- I provide this software for people to patch fonts for their own use. I don't support redistributing patched licensed fonts.


