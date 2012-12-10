# Eysys Front-End Coding Guidelines
*Last updated - 10/12/12*
We currently write CSS in [less](www.lesscss.org), vanilla javascript, and typically write [jade](http://jade-lang.com) that compiles to HTML and scala/japid/whatever java template language we're working on today.
This document has been written to keep track of the way we write our front-end code, to keep it as consistent as possible between developers & designers. 


### LESS
We currently use less because it's quick to learn, and is pretty much vanilla CSS with mixins and variables.

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
* Don't use `#id`s as hooks *ever*. Use semantically defined classes instead — e.g. `.header-nav`
* Prepend an underscore for javascript-specific classes, to be used alongside style classes. That way we can have one without the other. *Don't style javascript hooks* — e.g. `._js-hook .style-hook`
* Because CSS uses American spelling (e.g 'color'), for the sake of clarity use the american spelling in variables you might have — e.g. `@color-white` not `@colour-white` (you get used to it)
* Don't nest deeper than 3 levels
* When defining classes, put the most important definitions first (`position`, `display`…), and put nested elements at the end
* If nesting `@media` queries, put these after nested elements, right at the end of the definition.
* Definitions that are only 1 line are put inline — e.g. `.foo { display: none;}`
* Don't nest under `@media` queries. Instead, put an `// end` comment after the closing bracket.

#### Output
When outputting, compress in the YUI style (compressed down to 1 line, no whitespace). Make sure that `/*!` comments are in the output, but all other comments are excluded.
CodeKit's LESS compiler won't output standard `//` style comments, use that to your advantage.

#### Floats and clearfixes
As we're developing a lot of web apps, we're going to want to build navigations and interface elements that aren't straightforward to build in HTML and CSS. Using floats can be a effective method to get the kind of layouts we want, and we use a micro-clearfix hack to fix problems that floats cause. It looks like this:
    .cf() { // Micro ClearFix hack
        *zoom:1;
        &:before, &:after {
            content:"";
            display:table;
        }
        &:after { clear:both; }
    }
Use as a mixin by adding into elements that have floats within them — e.g. on a `ul` with floated `li` elements inside


### Jade/HTML
* Use HTML5 elements for semanticity, but use with CSS classes to style. Don't style the elements themselves — e.g. `header.top-toolbar`
* Make sure jade is compiled minified, otherwise whitespace could mess up your designs