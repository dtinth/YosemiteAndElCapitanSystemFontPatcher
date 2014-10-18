Yosemite System Font Patcher
============================

Change the system font of Mac OS X Yosemite.

<img src="http://i.imgur.com/I84LhWq.png" width="444.5" height="414.5" alt="Replacing the system font with Avenir next">


Prerequisites
-------------

Copy __HelveticaNeueDeskInterface.ttc__ from __/System/Library/Fonts/__ to the root of the repository.

Install FontForge with Python support.

```bash
brew install fontforge --with-python
```

Make sure FontForge works:

```python
>>> import fontforge
>>> fontforge
<module 'fontforge' from '/usr/local/lib/python2.7/site-packages/fontforge.so'>
```


