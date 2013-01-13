---
title: Photoshop .aco to UIColors
date: '2013-01-13'
description: Converting Adobe Photoshop .aco palette files to hex color codes. 
categories: photoshop, color, palette, 

---

Photoshop .ACO color palettes are probably the easiest way to get a color
list from a designer, but getting those colors isn't all that
easy. Adobe at least doesn't provide a tool (that I'm aware of at
least) that will export colors into a more accessible form.

What I wanted was a tool which would export an .aco to a plain text datafile,
 I found something quite close in the form of
[aco2html](http://www.hping.org/aco2html/).

My specific use case was to make Objective C / Cocoa `UIColor` so I
grabbed the code and
[made this](https://github.com/jasonm23/photoshop-aco2UIColors). 

This version generates a list of `UIColor` object values (undeclared),
which can be quickly assigned to variables, I also tacked on hex and
css `rgb()` colors. 

[UIColor colorWithRed:0.658824 green:0.639216 blue:0.556863 alpha:1.0f], // #a8a38e  rgb(168,163,142) 
[UIColor colorWithRed:0.513726 green:0.486275 blue:0.403922 alpha:1.0f], // #837c67  rgb(131,124,103) 
[UIColor colorWithRed:0.913725 green:0.709804 blue:0.254902 alpha:1.0f], // #e9b541  rgb(233,181,65) 
[UIColor colorWithRed:0.792157 green:0.768627 blue:0.709804 alpha:1.0f], // #cac4b5  rgb(202,196,181) 
[UIColor colorWithRed:0.901961 green:0.886275 blue:0.847059 alpha:1.0f], // #e6e2d8  rgb(230,226,216) 
[UIColor colorWithRed:0.254902 green:0.227451 blue:0.180392 alpha:1.0f], // #413a2e  rgb(65,58,46) 
[UIColor colorWithRed:0.400000 green:0.380392 blue:0.313726 alpha:1.0f], // #666150  rgb(102,97,80) 
[UIColor colorWithRed:0.560784 green:0.537255 blue:0.458824 alpha:1.0f], // #8f8975  rgb(143,137,117) 

This was a couple of months ago, and looking back integrating the
templating was a bad move. although using `cut` it's not too
difficult to extract the color values.

To get the `rgb()` colors only:

    cat example.aco | aco2UIColors | cut -c86-
    
To grab the hex colors:

    cat example.aco | aco2UIColors | cut -c77-84
    
To get the decimal triplets, red, green, blue (0.0 - 1.0) 

    cat example.aco | aco2UIColors | cut -c19-60 

At some point I'll update this so it optionally spits out the colors
as a JSON tree.

