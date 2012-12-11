# Eysys Front-End Coding Guidelines
*Last updated - 10/12/12*
We currently write CSS in [LESS](www.lesscss.org), vanilla javascript, and typically write [jade](http://jade-lang.com) that compiles to HTML/rythm.
This document has been written to keep track of the way we write our front-end code, to keep it as consistent as possible between developers & designers. 


### LESS
We currently use LESS because it's quick to learn, and is pretty much vanilla CSS with mixins and variables.

#### Units
Pixel-perfect designs no longer exist. We design for *The Web*, which means that our designs are going to be viewed on an infinite number of screen sizes with an infinite number of pixel densities. With that in mind:

* Use percentages for layouts
* Use `em`s for pretty much everything - including `@media` queries
* Only use pixels for stylistic effects, not stuff like positioning — e.g. `text-shadow` and `box-shadow`, not `top` and `margin`, and definitely not `@media` queries

#### To Start
* Use 4-space indents (not tabs)
* Keep line lengths under 80 chars where possible (exceptions are gradient syntaxes etc.)
* Make sure mixins are parametrically defined, with brackets. This makes sure they aren't outputted into the CSS — e.g. `.mixin()`

#### Naming and Defining Classes
* Keep names as short as possible as to still make sense — e.g. `.report-nav` not `.rprt-nav`, and `.sys-nav` not `.system-nav`
* Don't use `#id`s as styling hooks. Use semantically defined classes instead — e.g. `.header-nav`
* Keep styling classes separate fro javascript manipulation classes — e.g. `.report-preview.js-report-preview`. This means we *can* have one without the other.
* Because CSS uses American spelling (e.g 'color'), for the sake of clarity use the american spelling in variables you might have — e.g. `@color-white` not `@colour-white` (you get used to it)
* Don't nest deeper than 3 levels when using LESS. Not only does it make it easier to read, but it helps to keep selectors shorter, [optimising CSS parsing speed](https://speakerdeck.com/jonrohan/githubs-css-performance).
* When defining classes, put the most important definitions first (`position`, `display`…), and put nested elements at the end
* If nesting `@media` queries, put these after nested elements, right at the end of the definition.
* Definitions that are only 1 line are put inline — e.g. `.foo { display: none;}`
* Don't nest under `@media` queries. Instead, put an `// end` comment after the closing bracket so we can keep track of it.

#### Output
When outputting, compress in the YUI style (compressed down to 1 line, no whitespace). Make sure that `/*!` comments are in the output, but all other comments are excluded.
CodeKit's LESS compiler won't output standard `//` style comments, use that to your advantage. (Don't forget your attributions).

#### Floats and clearfixes
As we're developing a lot of web apps, we're going to want to build navigations and interface elements that aren't straightforward to build in HTML and CSS (static toolbars, window-in-window scrolling etc.). Using floats can be a effective method to get the kind of layouts we want, and we use a micro-clearfix hack to fix problems that floats cause. This is it:
    .cf() { // Micro ClearFix hack
        *zoom:1;
        &:before, &:after {
            content:"";
            display:table;
        }
        &:after { clear:both; }
    }
Use as a mixin by adding to elements that have floats within them — e.g. on a `ul` with floated `li` elements inside.


### Jade
We use [jade](jade-lang.com) because it means we can write really dry html. If you're lucky enough to have a mac with codekit installed, you can write html really quickly and see the results instantly.

* Use HTML5 elements for semanticity, but use with CSS classes to style. Don't style the elements themselves — e.g. `header.top-toolbar`
* Make sure jade is outputted minified, otherwise whitespace could mess up your designs
* Build with a base template that pulls all the layout together
	* Put the head contents in layout.jade, as an extendable `block`
	* Put a `body` `block` in as well
	* Each required page then extends `body` and `head` as required
* If you're re-using any elements (e.g. Save/Cancel button group), put that in a jade partial. This means we only have to edit one file if we want to make changes.