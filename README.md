# FontMake Issue #1080 Reproduction

*This issue has been resolved. See the Update below for details.*

Repo made for https://github.com/googlefonts/fontmake/issues/1080.

Running the following seems to do nothing, which is unexpected and seems to cause downstream problems:

```sh
fontmake -i -o ufo -g "New Font.glyphs"
```

Or rather, it outputs a response that appears to show things happening, but no files are actually output. Here's how it looks for me:

```sh
▶ fontmake -i -o ttf -g "New Font.glyphs"
INFO:fontmake.font_project:Building master UFOs and designspace from Glyphs source
INFO:glyphsLib.parser:Parsing .glyphs file
INFO:fontmake.font_project:Loading 1 DesignSpace source UFOs
INFO:fontmake.font_project:Interpolating master UFOs from designspace
```

But again, no UFO is output.

This also seems to be the case for other output types, such as TTF:

```sh
fontmake -i -o ttf -g "New Font.glyphs"
```

## UPDATE: the answer (for the simplified case, at least)

The Glyphs file in this repo didn’t yet include anything in the *Font Info > Exports*. Once an instance/export was added, the fontmake `-i` flag started working as expected.

So, this probably isn’t a FontMake issue, after all. 

(I am still experiencing this issue in a more complex font, but perhaps the real issue is again in the font, and I just need to find it. It isn’t as simple as the lack of a defined Instance, however.)

## Setup for reproduction

1. Git clone the repo, then move into it in a terminal.
2. Create and activate a virtual environment: `python3 -m venv venv && source venv/bin/activate`
3. Install fontmake: `pip install fontmake`

Then, you can run the commands described above.


## Further testing

The no-output behavior seems to be the case from FontMake `3.7.0` onward.

FontMake `3.6.0` does output a `master_ufo` folder for `fontmake -i -o ufo -g "New Font.glyphs"`.

However, even in `3.6.0`, if `-i -o ttf` options are specified, it doesn’t create any TTF, but only the `master_ufo` folder.
