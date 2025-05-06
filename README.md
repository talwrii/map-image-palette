# Edit an image by editing it's palette
**@readwithai** - [X](https://x.com/readwithai) - [blog](https://readwithai.substack.com/) - [machine-aided reading](https://www.reddit.com/r/machineAidedReading/) - [📖](https://readwithai.substack.com/p/what-is-reading-broadly-defined
)[⚡️](https://readwithai.substack.com/s/technical-miscellany)[🖋️](https://readwithai.substack.com/p/note-taking-with-obsidian-much-of)

Images often have a "palette", a set of colors that they use. You may wish to change the set of colors that are used by editing this palette. This is some python code to let you do this.

## Motivation and alternatives
I had a nice image I wanted to use, but I wanted to simplify it by reducing the number of colours. I wanted to do this in a controlled way rather than use [a posterize filter](https://docs.gimp.org/2.8/en/gimp-tool-posterize.html) but could not find any tools to do it.

GIMP has some limited ability to edit palettes through [its colormap dialogue](https://docs.gimp.org/3.0/en/gimp-indexed-palette-dialog.html), but as far as I can tell you can't copy colors between palette entries - only manually edit the hex code (and select regions with a certain color).

FFmpeg has the ability to generate palette files like we generate here with [palettegen](https://ffmpeg.org/ffmpeg-filters.html#palettegen) however it can only downsample to this palette, not replace colors.

I may have been able to got the effect I wanted by posterizing with a medium number of colors and then editing by hand using the colormap (which would be more feasible with a smaller number of colors).

## Some pages on this topic

1. [ImageMagick palette swap] (https://www.reddit.com/r/imagemagick/comments/17boqyn/how_to_replace_multiple_exact_colors_palette_swap/)
2. [Edit and reorder palette in GIMP](https://www.reddit.com/r/GIMP/comments/1kffkjx/edit_and_reorder_palette/)

## Caveat
You probably don't want to do this. You may well be able to get what you want using a "Posterize" filter in many editors and the colormap feature in GIMP (though I found this too fiddly to use).

I don't feel like this is a particularly efficient approach. If you know of a better approach (which I can validate and run without too much work) feel free to add it as an issue and I will linke to this here.

I coded this using Python inside emacs. A more standard approach would be to use a jupyter notebook. If I were to use this a lot, I would have this watch for changes to the palette and automatically update the display of the image.

## Usage
I made this tool in [emacs org-mode](https://orgmode.org/) using [babel](https://orgmode.org/worg/org-contrib/babel/intro.html) and [emacs-jupyter](https://github.com/emacs-jupyter/jupyter).

This is an equivalent to the more standard [jupyter](https://jupyter.org/) used for interactive data analysis. I would suggest using copying and pasting the code blocks here into jupyter rather than setting up emacs for normal users. I do not feel inspired to do so at the moment and sharing this code will be valueble.

Emacs users who know python can probably easily get this org babel file settings.

To use this tool, run the various pieces of python code (either in jupyter or emacs org-mode) -- see [edit-with-palette.org](edit-with-palette.org)

This will extract the palette from an image, write it to a file. If you copy this file, edit it, and store it in `palette-new.png` you can edit this file in GIMP, or another editor, then run the final commmand which uses this palette to create a new image with fewer colours.
