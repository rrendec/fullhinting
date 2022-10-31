# Font Rendering

These issues affect glyph rendering (the aspect of individual glyphs).

## Hinting Broken in Applications Using Webkitgtk

### Symptoms

The same glyph appears with different amount of hinting in the same line of
text, causing a very odd and blurry appearance. Some glyphs are fully hinted,
some look like they've been offset by a fraction of a pixel.

Known affected applications:
* [Epiphany](https://wiki.gnome.org/Apps/Web) - Web browser for the GNOME
  desktop
* [Evolution](https://wiki.gnome.org/Apps/Evolution) - GNOME mailer, calendar,
  contact manager and communications tool

### Resolution

Even though applications using webkitgtk seem to be affected, the issue is in
[Cairo](http://cairographics.org). The issue appeared in version 1.17.4 of the
library, and hasn't been addressed so far.

For now, the solution is to revert (downgrade) to an older version of Cairo.

### References
* [RHBZ 1999078 - Hinting strangely broken in Epiphany](https://bugzilla.redhat.com/show_bug.cgi?id=1999078#c24)
* [Cairo Issue #511 - Subpixel positioning sometimes screws up hinting](https://gitlab.freedesktop.org/cairo/cairo/-/issues/511)

# Font Spacing

These issues affect the spacing between glyphs.

## Bad Font Spacing in all GTK3 Widgets

### Symptoms

The issue appears only when full hinting is enabled. The space between some of
the glyphs is larger than expected, making the overall text width larger.

### Resolution

Even though it seems to affect all applications using GTK3, the issue is in
[Pango](http://www.pango.org). The issue appeared in version 1.44 of the library
and was fixed somewhere before version 1.50. Then it reappeared in version
1.50.3.

For now, the solution is to downgrade the library to an older version - either
version 1.43 or version 1.50.2, depending on the current/affected version of the
library.

### References

* [Pango Issue #404 - Bad font rendering with 1.44](https://gitlab.gnome.org/GNOME/pango/-/issues/404)
* [Pango Issue #656 - Horizontal spacing regression in 1.50.3](https://gitlab.gnome.org/GNOME/pango/-/issues/656)
