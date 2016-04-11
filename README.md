# JigSass Utils Float
[![NPM version][npm-image]][npm-url]  [![Dependency Status][daviddm-image]][daviddm-url]   

 > Float-related utility classes


Class names follow the [Emmet](http://docs.emmet.io/cheat-sheet/) abbreviation
syntax, with colons (':') replaced by two dashes (`--`) to follow BEM naming
conventions.

## Available classes

  - `.u-fl--start`: float: (left|right) (left in `LTR`, right in `RTL`)
    - `[dir=ltr] .u-fl--start`: float: left
    - `[dir=rtl] .u-fl--start`: float: right
  - `.u-fl--end`: float: (right|left) (right in `LTR`, left in `RTL`)
    - `[dir=ltr] .u-fl--end`: float: right
    - `[dir=rtl] .u-fl--end`: float: left
  - `.u-fl--n`: float: none
  - `.u-fl--l`: float: left
  - `.u-fl--r`: float: right

  - `.u-cl--start`: clear: (left|right) (left in `LTR`, right in `RTL`)
    - `[dir=ltr] .u-cl--start`: clear: left
    - `[dir=rtl] .u-cl--start`: clear: right
  - `.u-cl--end`: clear: (right|left) (right in `LTR`, left in `RTL`)
    - `[dir=ltr] .u-cl--end`: clear: right
    - `[dir=rtl] .u-cl--end`: clear: left
  - `.u-cl--b`: clear: both
  - `.u-cl--n`: clear: none
  - `.u-cl--l`: clear: left
  - `.u-cl--r`: clear: right

## Installation

Using npm:

```sh
npm i -S jigsass-utils-float
```

## Usage
Import JigSass Utils Float into your main scss file near its very end, together with all
other utilities (utilities should always be the last to be imported).

```scss
@import 'path/to/jigsass-utils-float/scss/index';
```

Like all other JigSass Utils, JigSass Float does not automatically generate any CSS
when imported. You would need to explicitly indicate that each individual float or clear
class should actually be generated in each component or object it is used in
(clarification: This will include style declarations inside `.foo` and .`bar`):

```scss
// _c.foo.scss
.foo {
  @include jigsass-util(u-fl, $modifier: n); // <-- float: none;

  ...
}
```

```scss
// _c.bar.scss
.bar {
  @include jigsass-util(u-cl, $modifier: b);  // <-- clear: both
  @include jigsass-util(u-cl, $modifier: r, $from: large); // <-- clear: right from large bp and on.

  ...
}
```

Doing so helps us a great deal with portability, as no matter where we import component or object
partials, the correct utility classes will be generated. Think of it as a poor man's dependency
management.

Developer communication is also assisted by including "dependencies" wherever they are required,
as anyone going through a partial, can easily understand how it should be marked up with just a
glance.

As far as bloat goes, just don't worry about it - the actual styles will only be generated once,
at the location in the cascade where the Jigsass Float partial was imported into the main file.


JigSass Float classes are responsive-enabled, using [JigSass MQ](https://txhawks.github.io/jigsass-tools-mq/)
and the breakpoints defined in the [$jigsass-breakpoints](https://txhawks.github.io/jigsass-tools-mq/#variable-jigsass-breakpoints) variable.

Based on the breakpoint arguments passed to `jigsass-util` when including a float or clear class,
responsive modifiers are generated according to the following logic:

```scss
.u-fl--<modifier>[-[-from-<breakpoint-name>][-until-<breakpoint-name>][-misc-<breakpoint-name>]]
```

So, assuming the `medium`, `large` and `landscape` breakpoints are defined in `$jigsass-breakpoints`
as `600px`, `1024px` and `(orientation: landscape)` respectively,

```scss
@include jigsass-util(u-fl, $modifier: end);
```
will generate the `.u-fl--end` class, which is not limited to any media-query.

```scss
@include jigsass-util(u-fl, $modifier: start, $until: medium);
```

will generate the `.u-fl--start--until-medium` class, which will be in effect at
`(max-width: 37.49em)` and will override styles in the default class until that point.

```scss
@include jigsass-util(u-fl, $modifier: c, $from: large, $misc: landscape);
```

will generate the `.u-fl--c--from-large-when-landscape` class, which will go into
effect at `(min-width: 64em) and (orientation: landscape)` and will override styles in the default
class under these  conditions.



## Documentation

The full documentation was generated using mdcss, and is available at 
[https://txhawks.github.io/jigsass-utils-float/](https://txhawks.github.io/jigsass-utils-float/)

## Contributing

It is a best practice for JigSass modules to *not* automatically generate css on `@import`, but 
rather have the user explicitly enable the generation of specific styles from the module.

Contributions in the form of pull-requests, issues, bug reports, etc. are welcome.
Please feel free to fork, hack or modify JigSass Float in any way you see fit.

#### Writing documentation

Good documentation is crucial for usability, scalability and maintainability. When 
contributing, please do make sure that both its Sass functionality (functions, mixins, 
variables and placeholder selectors), as well as the CSS it generates (selectors, 
concepts, usage exmples, etc.) are well documented.

Jigsass Float uses Jonathan Neal's [mdcss](//github.com/jonathantneal/mdcss).

When styles and documentation comments are not automatically generated by your module on `@import`,
please use the `sgSrc/sg.scss` file to enable their generation.

In addition, any file in `sgSrc/assets` will be available for use in the style guide.



## File structure
```bash
┬ ./
│
├─┬ scss/ 
│ └─ index.scss # The module's importable file.
│
├─┬ sgSrc/      # Style guide sources
│ │
│ ├── sg.scc    # It is a best practice for JigSass 
│ │             # modules to not automatically generate 
│ │             # css and documentation on `@import.` 
│ │             # Please use this file to enable css
│ │             # and documentation comments) generation.
│ │
│ └── assets/   # Files in `sgSrc/assets` will be 
│               # available for use in the style guide
│
└─┬ docs/      # Documention
  │
  └── styleguide/ # Generated documentation 
                  # of the module's CSS
```


**License:** MIT



[npm-image]: https://badge.fury.io/js/jigsass-utils-float.svg
[npm-url]: https://npmjs.org/package/jigsass-utils-float

[daviddm-image]: https://david-dm.org/TxHawks/jigsass-utils-float.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/TxHawks/jigsass-utils-float
