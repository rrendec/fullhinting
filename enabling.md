# Enabling full hinting

The actual font rendering is done by the [FreeType](https://freetype.org/)
library. It is responsible for reading True Type font files (ttf) and drawing
text according to the instructions. True Type fonts are basically vector
graphics, and they need to be converted into a bitmap to be displayed on the
screen. This process is called rasterization.

It is worth noting that partial hinting or slight hinting also exists. In that
case, glyphs are still aligned to the screen pixel grid, but they are not fully
aligned. Horizontal and vertical lines (for example letters H and T) may not
perfectly overlap with the pixel grid and create shadows in the adjacent pixels
due to antialiasing. With full hinting horizontal and vertical lines are always
fully aligned with the pixel grid.

## True Type interpreter version

The FreeType library has multiple versions of the font rendering engine, all
coexisting in the same library version. They are called interpreter versions.
Currently, v35 and v40 are included, and v40 is the default.

The problem is that v40 does not seem to support full hinting. To be able to use
full hinting, the FreeType library must be configured to use v35.

To change the setting for your user only (recommended), create the `.profile`
file in your home directory (if it doesn't already exist) and add the following
line:

```sh
export FREETYPE_PROPERTIES="truetype:interpreter-version=35"
```

Log out of your graphical desktop session and log back in to apply the setting.

## Fontconfig library configuration

[Fontconfig](https://www.freedesktop.org/wiki/Software/fontconfig/) is a library
designed to provide a list of available fonts to applications, as well as
configuration for how fonts get rendered. The FreeType library renders fonts
based on this configuration.

Fontconfig is very flexible. In addition to default rendering parameters, it can
be configured to provide customized rendering parameters based on various
properties of the font, such as family, weight, etc.

At the system level, Fontconfig is configured in `/etc/fonts/fonts.conf` and
`/etc/fonts/conf.d/`. At the user level, Fontconfig is configured in the
`.config/fontconfig/fonts.conf` in the user's home directory.

To enable full hinting, add the following settings to the Fontconfig
configuration. It is recommended to use the user level configuration.

```xml
    <match target="font">
        <edit name="antialias" mode="assign">
            <bool>true</bool>
        </edit>
        <edit name="hinting" mode="assign">
            <bool>true</bool>
        </edit>
        <edit name="hintstyle" mode="assign">
            <const>hintfull</const>
        </edit>
        <edit name="rgba" mode="assign">
            <const>none</const>
        </edit>
        <edit name="autohint" mode="assign">
            <bool>false</bool>
        </edit>
        <edit name="lcdfilter" mode="assign">
            <const>lcdnone</const>
        </edit>
    </match>
```

## Not all fonts are the same

The font rendering engine cannot figure out by itself which parts of the glyphs
need to be aligned to the pixel grid and how to align them. Specific instructions
must exist in the True Type font to support hinting, and not all fonts have them.

Part of the configuration is to use a font that supports full hinting. The
configuration can be done in several different places:
* In the desktop environment. Most desktop environments have font settings that
  affect widget rendering (window titles, menus, buttons, etc.) and the default
  font choice for text rendering in other areas of the applications.
* In the application. For example, web browsers have additional font settings
  that override the desktop environment settings and control font rendering
  inside web pages.
* In the Fontconfig library configuration. Fontconfig is responsible not only
  for providing the FreeType rendering settings to applications, but also for
  providing an actual existing font to be used when the application requests a
  font family (rather than a specific font), or a font that doesn't exist on the
  system.

The following font families are known to support full font hinting:
* **DejaVu**
* **Liberation**, version 1. Full hinting support was dropped in version 2.
