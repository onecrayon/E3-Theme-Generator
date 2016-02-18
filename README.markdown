# E3 Theme Generator template

This project provides an SCSS template for generating syntax themes for [Espresso 3](http://macrabbit.com/espresso/), along with ports of my two original Espresso themes (Earthworm and Quiet Light)--both as examples for using the template, and for use with Espresso 3.

## Installing and using Earthworm or Quiet Light

1. Download the CSS files in the `ThemeGenerator/OneCrayon` folder and move them into your Themes folder:
    
        ~/Library/Application Support/Espresso/Themes
2. Relaunch Espresso, if it is open, and choose Earthworm or Quiet Light in the Colors preferences

## Creating your own theme

1. Download or clone the project, and open the folder in Espresso 3.
2. Duplicate the `ThemeGenerator.esdynamo/_template.scss` file, and rename it `MyThemeName.scss`
3. Modify your new SCSS file (see below), then move `ThemeGenerator/MyThemeName.css` into the Espresso Themes folder as per above, or create a symlink to it like so:
    
        cd ~/Library/Application\ Support/Espresso/Themes
        ln -s path/to/E3-Theme-Generator/ThemeGenerator/MyThemeName.css MyThemeName.css

### Modifying the template

When you open your renamed copy of `_template.scss` you will find a long list of variables, most of which are commented out. The uncommented variables are required in order to have a bare minimum working theme, while the others allow you to override colors for common elements on a per-language basis.

There are two types of variables:

* Variables at the top of the file are what-you-see-is-what-you-get, and do not support suffixes for adjusting font-weight and similar
* The next set of variables allow you to modify several properties by adding variants with suffixes. For instance, although only these variables are listed:
    
        $comment: #000;
        $string: #000;
    
    You can still modify the font weight, style, background color, and background opacity for these zones by adding variables with the appropriate suffix:
    
        $comment: #000;
        $comment-weight: bold;
        $comment-style: italic;
        $comment-background: #fff;
        $comment-background-opacity: .4;
        
        $string: #000;
        $string-weight: bold;
        $string-style: italic;
        $string-background: #fff;
        $string-background-opacity: .4;

### Available variables

Most of the variables should be fairly self-explanatory, but here are some notes:

* **$text**: default text color across the application
* **$background**: default background color across the application
* **$current-line**: background color for the current line highlight (whether this shows up or not is chosen by the user)
* **$embedded-\***: these set the colors and backgrounds for the given languages when embedded within HTML documents
* **$monotone-property-values**: uncommenting this variable will cause constants and keywords in CSS property values to be colored the default `$property-value` color (functions like `rgba()` will still be colored using the `$function` color, so if you want completely monotone property values you will need to set `$css-function: $property-value;`, as well)
* **$function** vs. **$function-call**: these refer to the function name when the function is declared (`$function`) vs. when it is invoked (`$function-call`). If `$function-call` is not set, it will default to the same color as `$function`, so set `$function-call: $text;` if you want it to remain uncolored. These variables also color classes and modules in PHP, Python, and Ruby.
* **$php-delimiter** (and other **$\*-delimiter** variables): these color the delimiters for the language itself when embedded elsewhere: `<?php` and `?>`. `$ruby-delimiter` is only used for ERB documents. Similarly, `$regex-delimiter` only highlights the characters that form the boundaries of the regular expression (so `/` in Javascript, for instance).

### Miscellaneous notes

* Setting the required variables will get you a basic minimum theme, but in order to properly support all languages you will also want to color at least a few of the Markdown and Regex variables (otherwise both languages will end up largely colorless, since their basic zones are a bit different than the other languages).
* If you wish to support third-party languages, you can add selectors for them beneath the import statement at the bottom of the template file (see Earthworm and Quiet Light for some examples of how this works).
* Espresso's syntax system offers a lot more granular control than this template offers! If you would like to target other zones, you can do that beneath the import statement, as well (Quiet Light has some good examples of this). You can find full documentation on themes in the [Espresso wiki](http://wiki.macrabbit.com/SyntaxThemes/).

## MIT License

Copyright (c) 2016 Ian Beck

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
