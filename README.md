# pdf2keynote

Convert a PDF, for example a LaTeX/Beamer talk, into a Keynote presentation:
one PDF page per slide, placed full-bleed as a vector image. You keep writing
the talk in LaTeX and present it from Keynote (presenter display, remote,
rehearsal timing).

It replaces the old PDF2Keynote.app, which no longer works with current
Keynote versions.

## Requirements

- macOS with Keynote installed (tested: macOS 26.6, Keynote 14.5)
- nothing else: the tool is a single JavaScript-for-Automation script run by
  the built-in `osascript`, and uses macOS's own PDFKit

## Install

```sh
git clone https://github.com/pbeerli/pdf2keynote.git
ln -s "$PWD/pdf2keynote/pdf2keynote" ~/bin/pdf2keynote   # any folder on your PATH
```

The first run asks for permission to control Keynote (System Settings →
Privacy & Security → Automation); allow it for your terminal app.

## Usage

```sh
pdf2keynote talk.pdf                  # writes talk.key next to the PDF
pdf2keynote talk.pdf -o slides.key    # choose the output file
pdf2keynote talk.pdf --width 1024     # slide width in points (default 1920)
```

The slide height follows the aspect ratio of the first PDF page. A page with
a different shape is scaled to fit and centred.

## How it works

1. PDFKit splits the PDF into one-page PDFs in a temporary folder.
2. Keynote creates a document with the slide size, adds a blank slide per
   page and places the page on it. Keynote keeps PDF images as vectors, so
   text and lines stay sharp at any size.
3. The page's text is stored as the image description, so VoiceOver can read
   each slide.
4. The document is saved and the temporary folder removed.

## Limitations

- Each slide is one picture: there are no Keynote builds or transitions, and
  links in the PDF are not clickable.
- Presenter notes are not transferred.
- An existing output file is replaced.

## License

MIT, see [LICENSE](LICENSE).
