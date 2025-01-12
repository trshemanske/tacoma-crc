# A roadmap for modifications to produce a crc-like theme

## Introduction

The goal of this modified theme was to achieve a crc-like feel while not
modifying any of the core components of the CSS generation system directly,
and which will hopefully be portable between PreTeXt versions.

The _centered_ part of the crc theme was already implicit in the tacoma theme,
leaving only rounded corners, fonts, and some colors to play with.

To start, I simply cloned the tacoma theme folder, and ended up renaming:
`theme-tacoma.scss` to `theme-tacoma-crc.scss`, and similarly for `_parts-tacoma.scss`, the
former since this was obviously a newish theme and the second since I wanted to pass a
new variable to one of the `@use` components.

At first, I was hopeful that the rounded corners would be handled by the
ubiquitous `$border-radius` statements as a pass through to other components, and
while that might be possible, I wasn't successful.

## theme-tacoma-crc.scss

For example, in `theme-tacoma-crc.scss`, I tried the following with no apparent effect:

    $border-radius: 8px !default;

    //@use 'chunks-minimal' with ($border-radius: 0);
    @use 'chunks-minimal' with ($border-radius: $border-radius);

In `theme-tacoma-crc.scss` I made the following changes:

Change primary color which sets the color for title font, by-line font, links,
etc. Set it to be red, and it is easy to see what gets changed!

      //$primary-color: #015d74 !default;
      $primary-color: #014d60 !default; // var(--bluegreen-dark)

I had to change
`@use 'parts-tacoma' as parts;` to `@use 'parts-tacoma-crc' as parts;`.

I wanted a sans-serif font in general, so I borrowed the following from the
`denver` theme:

      // @use 'fonts/fonts-google';

      // crc modification: taken from denver theme
      $heading-font: "Noto Sans, Helvetica Neue, Helvetica, Arial, sans-serif" !default;
      @use "fonts/fonts-google" with (
      $heading: $heading-font
      );

## \_parts-tacoma-crc

To make the footer navigation buttons rounded, I added the definition:

    $footer-button-border-radius: 8px !default;
     @use 'components/page-parts/body' with (
    **_ previous content _**,

    $footer-button-border-radius: $footer-button-border-radius,
    );

## \_customization.scss

This is where the bulk of the modifications take place.

I freely admit that determining what CSS to modify was an exploration, often
simply looking at the HTML page source of an element I wanted to style,
determining all the classes that modified it, and the grepping my way through
all the components, chunks, helpers, etc. to find appropriate code to modify.

As you can see by reading the file, most changes were to anchor tags, changing
border-radius, font color and size as well as changes when the link is
active/hovered.

## publication.ptx

My publication file has the line:
<css theme="custom" entry-point="tacoma-crc/theme-tacoma-crc.scss" />

where `tacoma-crc` is a symbolic link to my theme development directory, and is
located in the source directory of the project.  This has the advantage of not 
creating a dependence on the PreTeXt version.

## \_chunks-minimal.scss

This file was unchanged from the tacoma theme. Andrew Scholer offered the
following advice:

Any `@use` in custom SCSS will search two paths for matching files. Relative 
to the file, and starting from css/ in the pretext source (e.g.,
`~/.ptx/<version>/core/css/`). 

So, since the tacoma-crc `_chunks-minimal` file has no changes from the copy 
in the original tacoma theme, you could delete your copy of `_chunks-minimal` 
and in your `theme-tacoma-crc.scss` file, change:

`@use 'chunks-minimal' with ($border-radius: 0);`
to
`@use 'targets/html/tacoma/chunks-minimal' with ($border-radius: 0);`

Since there is no local 'targets/...' folder, the one that would get found by 
that @use is the one in `~/.ptx/.../css/`.

Keeping a copy of tacoma's `_chunks-minimal` in the tacoma-crc directory has 
the advantage of "locking in" what the chunks look like, so you are not affected 
by any changes to the tacoma version of that file. 

Linking to the main tacoma/chunks guarantees you automatically get any 
updates/fixes made to that file. 

Andrew's recommendation is to copy only things that require modification and 
link to anything that isn't changed.
