# Styles

### Organization

We split our styles into 6 main folders.

```
/styles
    /base
    /layouts
    /utils
    /objects
    /vendor
    /vendor-customization
    main.scss
```

#### /styles

Should only contain `.scss` files that you want to compile into separate `.css`files (usually only `main.scss`). All other `.scss` files should be in the appropriate folders.

#### /styles/base

Contains all of the global stylesheets used in the project.

#### /styles/layout

Includes all layout styles, which should always be prefixed with `l-`, such as `_l-site-footer.scss`. See the CSS section for more on layout files

#### /styles/objects

Includes all individual _objects_ (referred to in some frameworks as _modules_ or _components_). An object is a self-contained element or group of elements. See the CSS section for more on objects.

#### /styles/vendor

Ideally, all vendor styling assets should be handled via a package manager, but in the event that this is impossible or problematic a `/vendor` directory is appropriate. The `/vendor` directory should consist only of other directories, e.g. `/magnific-popup` or `/chosen`. _Do not_ drop unorganized stylesheets, images, or js into this directory.

#### /vendor-customization

Many libraries, such sliders, lightboxes, and interactive components need to have their styles customized for the project. These customizations should go in `/vendor-customization`. Never, _ever_ customize the appearance of a libraries elements by editing its original stylesheets. This will almost certainly make any future updates to the library difficult or impossible.


#### /styles/utils

Utility styles as well as functions and mixins. By default we include a few utilities that have proved useful on past projects.

### Files

#### /styles/main.scss

This is the entry point to your project's styles, and it should contain only `@import` statements.

Example:

```scss
// Vendor
@import "bower_components/susy/susy";
@import "bower_components/breakpoint/breakpoint";
@import "bower_components/slick/slick";

@import "vendor/normalize";
@import "vendor/reset";

// Vendor Customization
@import "vendor-customization/**/*";

// Utils
@import "utils/font-face";
@import "utils/font-family";
@import "utils/space";
@import "utils/color";

// Base
@import "base/typography";
@import "base/base";

// Objects
@import "objects/**/*";

// Layout
@import "layout/**/*";


```

#### /styles/vendor/_normalize.scss

[https://github.com/necolas/normalize.css](https://github.com/necolas/normalize.css)

Based on researching the differences between default browser styles, normalize makes browesers render all elements more consistently. This file can alternatively be pulled in via Bower.

#### /styles/vendor/_reset.scss

[http://meyerweb.com/eric/tools/css/reset/](http://meyerweb.com/eric/tools/css/reset/)

Removes many default CSS styles that are likely to be set uniquely for each project, such as margins, padding, type-sizes, and indentation. This file can alternatively be pulled in via Bower.

#### /styles/base/_variables.scss
File for _all_ variables.

#### /styles/base/_base.scss
Contains styles applied to bare elements (`p`, `a`, `ul`, etc.)

#### /styles/util/_color.scss

Contains a few useful color related functions. Check out the example file for a bit more information about what they do.

#### /styles/base/_helpers.scss

Helpers are classes that are intended to be used directly in the markup to handle common styling. Each helper should be _very_ limited in scope, typically affecting only a single CSS property, such as setting visibility or adding a border. Helpers should always be prefixed with `h-`, such as `.h-visually-hidden`

```scss
/* ==============================================================
   Helpers
   ============================================================== */

.h-not-displayed {
  display: none;
}

.h-visually-hidden {
  border: 0;
  clip: rect(0 0 0 0);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
}
```

#### /styles/global/_base.scss

Very limited universal defaults, such as setting `box-sizing: border-box`

```scss
/* ==============================================================
   Base
   ============================================================== */


// A very limited set of global defaults and styles

// Box Sizing Border-box
// ==============================================================

* { box-sizing: border-box; -moz-box-sizing: border-box; }.
```

### Code Style & Best Practices

We've found the following CSS guidelines to lead to more readable, maintainable code. Many of these rules are adopted from other sources, including [Harry Roberts](http://cssguidelin.es), [Jonathan Snook](http://smacss.com/), [Philip Walton](http://engineering.appfolio.com/2012/11/16/css-architecture/),[Hugo Giraudel](http://sass-guidelin.es/), and [Nicolas Gallagher](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/).

#### Basic Syntax & Formatting

* Roughly 80 character line lengths
* 2 spaces for indentation
* Multi-line CSS Rules
* Separate rulesets with 1 empty line, and separate ruleset sections with 2 empty lines.
* Always wrap strings in single quotes
* `id` attributes in your markup are fine for non-css purposes (such as linking and javascript), but never use them as styling hooks.
* Never use the same classes you use for styling as javascript hooks. Instead, add `.js-` prefixed classes specifically for javascript, such as `.js-add-widget`
* Use `px` as a unit for precise details (like borders), `rem` for type, and `rem`, `em`, or percentages for everything else.
* Numbers should display leading zeros before a decimal value less than one.
* 0 values should not include units
* To add units to a number always multiply the nubmer by 1 unit.
* Always wrap calculations in parentheses
* Avoid magic numbers when possible, and always add a comment explaining them.
* Avoid nesting whenever possible, with the exception of closely-tied declarations like `:hover` or `:after`
* [Use indentation](http://cssguidelin.es/#indenting) to make the relationship between rulesets more clear.

```scss
// Yep
.foo {
  font-family: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif;
  opacity: 0.5;
  display: block;
  overflow: hidden;
  padding: 0 1em;
  width: (42 * 1px);
}

 // Nope
.foo {
  font-family: Helvetica Neue Light, Helvetica, Arial, sans-serif;
  opacity: .5;
  display: block; overflow: hidden;
  padding: 0em 1em;
  width: (42 + px);
}
```

#### Property Order

Ordering CSS properties consistently makes your styles easier to scan. Tools like [CSSComb](http://csscomb.com) make this easier.

* Sass `@include` statements
* Positioning
* Display/Visibility
* Floating
* Overflow
* Margin
* Padding
* Width/Height
* Outline/Border
* Background
* Text Alignment/Decoration
* Font Size
* Font Family

### Naming

One Design uses a CSS/html class-based naming convention adapted from the [BEM approach](https://en.bem.info/method/definitions/) (Block, element, modifier). This approach uses a verbose combination of hyphens (-) and underscores (_) to make relationships very clear. This results in more maintainable code by reducing selector specificity and eliminating naming collisions.

```scss
// The base (block)
// This corresponds with the outermost HTML element
// and typically represents an object or layout.

.person {}

// A child (element)
// There may be many of these inside of the block.

.person__head {}
.person__body {}

// A variant (modifier)
// The suffix is always added to the block name, never to an element name.

// Good:
.person--tall {}

// Bad:
// .person__head--tall {}

// Uniquely styling an element inside of a modified block:
.person--tall .person__head {}
```

When modifier classes are used in HTML, they are always used _in addition_ to the block class, not in place of it:

```html
<div class="person person--tall"></div>
```

### Objects

The vast majority of CSS and HTML we write is based around objects. An object represents a single small, reusable component like an avatar or form input. An object can also be made up of other objects. For instance, a profile object might contain an avatar and name, or a signup form object could contain multiple types of form input objects.

* Each object should have exactly one associated .scss file named to match the block name.
* The only time an object's styles should be touched in a file other than its main file is inside of a layout file (see Layouts below) or when contained in parent objects.
* The base object block should almost never have its width, margin, or height defined in its main file. These should be set in the layout or parent object that contains it and helps keep each object flexible. It's okay for sub-elements of the object to have these properties defined.
* An HTML element can not be more than one type of object. For instance, `<div class="user-profile sidebar-content">` is not allowed. As a general rule, all classes on an HTML element should be related to the same object, with the exception of Javascript hook (`.js-`) and Helper (`.h-`) classes.
* When including an object inside of another object (as in the `.avatar` exmaple below), you should create a child element to wrap that included object. This ensures that you have to touch the styles for the child object as little as possible.

```html
<div class="user-profile">
  <div class="user-profile__avatar">
    <img class="avatar" src="" alt="">
  </div>
  <div class="user-profile__details">
    <h2 class="user-profile__name">Eli Rosen</h2>
    <p class="user-profile__description">The quick brown fox jumped over the lazy dog…</p>
  </div>
</div>
```

```scss
// objects/_user-profile.scss

/* ==============================================================
   Profile
   ============================================================== */

/*
Profile

Contains information for a user.

.user-profile--large             - A larger version
.user-profile--condensed         - A brief version for tight spaces

Styleguide 1.1
*/

.user-profile {}

// Details

.user-profile__details {}
  .user-profile__name {}
  .user-profile__description {}


//---------------------------------------------------------------
// Included Modules
//---------------------------------------------------------------

.user-profile__avatar {}


//---------------------------------------------------------------
// Modifiers
//---------------------------------------------------------------

.user-profile--large {}
.user-profile--condensed {}
```

### Layout

The role of Layout files is to control the size and placement of objects (and other layouts), and occasionally apply things like background color and border to broad areas of a page.

* Each layout should have exactly one associated .scss file named to match the block name.
* Layouts follow the same general naming convention as objects, but with an `l-` prefix in front of the block and file name, e.g. `.l-header` and `_l-header.scss`
*   Layouts should never include typographic rules, such as `color`, `font-size`, `line-height`, etc.
* Layouts can contain other layouts, which makes it easy to compose complex layouts. For instance, its common to have an `.l-container` layout that always wraps everything else in the site, for the purpose of setting max width.
* Layouts are a good way to handle grid systems for a project, but try to avoid making super-generic grid layouts like `.l-grid-1-col`, `.l-grid-2-col`, `.l-grid-2-col`, etc. Instead, focus on making the minimum number of reusable layouts that are appropriate for your site design, such as `.l-main-with-sidebar`.
* Just like objects, layouts can have modifiers. So our `.l-main-with-sidebar` layout might have an `.l-main-with-sidebar--flipped` version that places the sidebar on the opposite side.

```html
<section class="l-container">
  <header class=“l-container__header”>
    <nav class="primary-nav"></nav>
  </header>
  <section class=“l-container__body">
    <div class="l-main-with-sidebar">
      <div class="l-main-with-sidebar__main"></div>
      <aside class="l-main-with-sidebar__sidebar"></aside>
    </div>
  </section>
</section>
```

```scss
// layout/_l-container.scss

/* ==============================================================
   Layout - Container
   ============================================================== */

/*
Layout - Container

The main wrapper for the entire site

Styleguide x.x.x
*/

.l-container {}

.l-container__header {}

.l-container__body {}
```

### Technology & Tools

 There are some common CSS challenges that we've found the following tools work well for:

 Grids: Susy
 [http://susydocs.oddbird.net/en/latest/](http://susydocs.oddbird.net/en/latest/)

Media Queries: Sass-MQ
[https://github.com/sass-mq/sass-mq](https://github.com/sass-mq/sass-mq)

Additionally, we prefer to avoid using the following tools & technologies:

* Compass (and any library or plugin with a Compass dependency)
* Foundation, Bootstrap, or any other kitchen-sink frontend framework.
