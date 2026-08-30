# Educational SVG

The shared drawing library for Teaching Plugins: 135,610 SVG drawings a lesson,
worksheet or working wall can reach for when a small relevant picture would help
a child.

## This repository is fetched, never cloned

A plugin does not clone this library. It ships a small index of every drawing's
name and pulls the individual files it actually chooses, which is usually a few
dozen per lesson.

That separation is the whole point of the repository existing on its own. The
drawings are about 940 MB across 135,610 files. Any repository people install a
plugin from carries that weight in its history for ever, on every install,
whether or not the files are still in the current folder. Keeping the drawings
out of those repositories is what keeps a plugin install quick.

So: add drawings here, and never copy the library into a plugin repository.

## Layout

```
library/<style>/<two-letter prefix>/<name>.svg
```

- `library/standard` (70,844)
- `library/cartoon` (62,258)
- `library/solid` (2,508)

The two-letter prefix folders keep each directory a manageable size while giving
every drawing a stable path. That path is the drawing's permanent identity, for
example `standard/ca/candle-lit.svg`, and it is what a lesson records when it
uses one.

A file name is the drawing's only description, so name a new drawing the way a
teacher would search for it: lowercase words separated by hyphens, the subject
first, `candle-lit.svg` rather than `lit_candle_01.svg`.

## Searching

Searching happens in the plugin, not here, because the plugin holds the index.
In Lesson v4:

```bash
node "[PLUGIN_ROOT]/scripts/search-educational-svg.js" --query "lit candle" --limit 12
```

## Adding drawings

Add the SVG at its proper path, then rebuild the index that plugins ship:

```bash
node "[PLUGIN_ROOT]/scripts/build-educational-svg-index.js" --library "library" \
  --out "[PLUGIN_ROOT]/educational-svg/index.br"
```

Commit the new drawings here and the rebuilt index in the plugin. A drawing that
is in this repository but missing from a plugin's index is invisible to that
plugin, and a name in the index with no file behind it fetches nothing and closes
the picture text-only. Neither breaks a lesson, but neither is much use either.

## Licence

The drawings arrived as a bulk set with no licence file. Until their terms are
established this repository stays private, and the library must not be published
or redistributed.
