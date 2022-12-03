# Font full hinting Support in Linux

The [Wikipedia article](https://en.wikipedia.org/wiki/Font_hinting) on font
hinting summarizes it very well:

> Font hinting (also known as instructing) is the use of mathematical
> instructions to adjust the display of an outline font so that it lines up with
> a rasterized grid. At low screen resolutions, hinting is critical for
> producing clear, legible text.

A picture is worth a thousand words. The image below shows the same text/font
rendered with full hinting (top) and no hinting (bottom).

![Full hinting and no hinting example](img/font_hinting-example.png "Font hinting example")

Simply put, font hinting makes fonts look crisp and thin, and whether this is
good or bad is highly subjective. It seems that the vast majority of people
simply go with whatever their OS default is and do not care or just cannot tell
the difference. Many others dislike font hinting, while others feel that font
hinting is the only way to make text easily readable and reduce eye strain. This
wiki is dedicated to enabling and supporting font full hinting in Linux.

In Linux, it used to be easy to either enable or disable font hinting, and this
worked pretty well out of the box around 2012. However, as the various libraries
that deal with font rendering have evolved and diverged, it is now very difficult
to consistently enable (or disable) font hinting across the entire desktop.

* [Enabling full hinting](enabling.md)
* [Debugging full hinting](debugging.md)
* [Known/active issues](issues.md)
* [External resources](resources.md)
