# tacoma-crc (working name changed to boulder as development continues)

A modification of the PreTeXt tacoma theme to include legacy-crc features.
Valid for PreTeXt 2.12.0 (and hopefully onward).

boulder is becoming a mix of other themes that exist, starting with tacoma, but
borrowing elements from others.  Centered-Rounded-Corners (crc) no longer really
makes sense since tacoma is centered for larger screen sizes.  I considered
minimally-rounded-corners, but the theme is not entirely spartan. It will
probably never be sufficiently polished to be a standard theme, but the idea is
to play and to give examples of how to modify exisiting themes.

## Introduction

Andrew Scholer accomplished an impressive rewrite of the CSS (generation) system for PreTeXt
documents, providing a uniform extensible platform on which new themes can be
built. Andrew, together with Oscar Levin, have created a number of new
themes to provide various presentation features desired by users of PreTeXt.

Some of these themes are new and others are in part revisions of legacy
themes. Among the legacy themes is the _crc_ theme (centered-rounded-corners) of
which I was quite fond. As we know, legacy today becomes deprecated tomorrow,
so I thought I would try to create something which captured key elements of the
crc theme.

To that end, I started with the Scholer's tacoma theme ("a minimal distraction
reading environment") which has a nice, light feel to it, and introduced changes
affecting fonts, base colors, and of course rounded corners which creates a
blend of the tacoma and crc features.

These changes simply provide a superficial new skin to the tacoma theme
affecting only CSS, so there should be no functional differences between tacoma
and tacoma-crc.

## Disclaimer

Andrew's new CSS generating platform is a complex mixture of elements organized
via SASS and many other things of which I know almost nothing. But of course why
would I let not understanding something interfere with tinkering with it. Hmm,
what does this red button do?

The modifications that are included will probably make Andrew and Oscar cringe,
because I was trying to create an end result, rather than leveraging the inherent
structure of this system, which I may yet figure out.

So my approach to constructing this modified theme was lots of viewing source of
generated html, noting all relevant tags for CSS classes and grepping my way
through all of Andrew's core documents to find the right elements to tweak.

This is far from a polished standalone theme. Still I hope it may encourage
others to play.

## Road Map Coming

While the files have reasonable inline documentation, I will try to include a
roadmap which indicates how various pieces were altered to achieve the desired
result.
