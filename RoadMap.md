# A roadmap for modifications to produce a crc-like theme

## Introduction

The goal here was to achieve a crc-like feel while not modifying any of the core
components directly, and so hopefully be portable between PreTeXt versions.

The _centered_ part of the crc theme was already implicit in the tacoma theme,
leaving only rounded corners, fonts, and some colors to play with.

To start, I simply cloned the tacoma theme folder, and ended up renaming:
`theme-tacoma.scss` to `theme-tacoma-crc.scss`, and similarly for `_parts-tacoma.scss`, the
former since this was obviously a newish theme and the second since I wanted to pass a
new variable to one of the `@use` components.

At first I was hopeful that the rounded corners would be handled by the
ubiquitous `$border-radius` statements as a pass through to other components, and
while that might be possible, I wasn't successful.

## theme-tacoma-crc.scss

For example, in theme-tacoma-crc.scss, I tried the following with no apparent effect:

    $border-radius: 8px !default;

    //@use 'chunks-minimal' with ($border-radius: 0);
    @use 'chunks-minimal' with ($border-radius: $border-radius);


In theme-tacoma-crc.scss I made the following changes:

  Change primary color which sets the color for title font, by-line font, links,
  etc. Set it red, and it is easy to see what gets changed!

      //$primary-color: #015d74 !default;
      $primary-color: #014d60 !default; // var(--bluegreen-dark)

  I had to change
  `@use 'parts-tacoma' as parts;` to `@use 'parts-tacoma-crc' as parts;`.

  I wanted a sans-serif font in general so I followed the following from the
  `denver` theme:

      // @use 'fonts/fonts-google';

      // crc modification: taken from denver theme
      $heading-font: "Noto Sans, Helvetica Neue, Helvetica, Arial, sans-serif" !default;
      @use "fonts/fonts-google" with (
      $heading: $heading-font
      );

## _parts-tacoma-crc

To make the foot navigation buttons rounded, I added the definition:

    $footer-button-border-radius: 8px !default;
     @use 'components/page-parts/body' with (
    **_ previous content _**,

    $footer-button-border-radius: $footer-button-border-radius, 
    );

## _customization.scss

This is where the bulk of the modifications take place.

I freely admit that determining what CSS to modify was an exploration, often
simply looking at the html page source of an element I wanted to style,
determining all the classes that modified it, and the grepping my way through
all the components, chunks, helpers, etc to find appropriate code to modify.

As you can see by reading the file, most changes were to anchor tags, changing
border-radius, font color and size as well as changed when the link is
active/hovered.

## publication.ptx

My publication file has the line:
<css theme="custom" entry-point="ptx-link/2.11.4/core/css/targets/html/tacoma-crc/theme-tacoma-crc.scss" />

where `ptx-link` is a symbolic link to my .ptx directory (~/.ptx) for me, and is
located in the source directory of your project, and where of course your have
created/transferred the tacoma-crc to the appropriate target directory.