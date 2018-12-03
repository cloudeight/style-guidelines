# Style Guidelines: CSS
> *A set of guidelines to CSS.*
<br />

## Table of Contents
1. [Introduction](#introduction)
2. [Foundation](#foundation)
3. [Syntax and Formatting](#syntax-and-formatting)
    - [Fundamentals](#fundamentals)
    - [Extended](#extended)
    - [Shorthand vs Longhand](#shorthand-vs-longhand)
    - [Multi-line Property Values](#multi-line-property-values)
    - [Vendor Prefixes](#vendor-prefixes)
4. [Naming Conventions](#naming-conventions)
    - [File Names](#file-names)
    - [BEM](#bem)
    - [Hooks](#hooks)
        - [State Hooks](#state-hooks)
        - [JavaScript Hooks](#javascript-hooks)
    - [Modifiers](#modifiers)
        - [Size Modifiers](#size-modifiers)
        - [Color Modifiers](#color-modifiers)
        - [Feedback Modifiers](#feedback-modifiers)
5. [SASS](#sass)
    - [Variables](#variables)
    - [Maps](#maps)
    - [Mixins and Functions](#mixins-and-functions)
    - [Declaration Order](#declaration-order)
    - [Conditional Statements](#conditional-statements)
    - [Partials](#partials)
6. [Commenting](#commenting)
    - [Headings](#headings)
    - [Inline](#inline)
    - [DocBlocks](#docblocks)
        - [Basics](#basics)
        - [Reference Subjects](#reference-subjects)
        - [SASS Annotations](#sass-annotations)
        - [Number Labels](#number-labels)
        - [Ordering](#ordering)
    - [Single Line](#single-line)
7. [Attributions](#attributions)


## Introduction
This is a style guideline for CSS that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to write CSS for your projects and we're always happy for insights, feedback, improvements and recommendations to help improve it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.


## Foundation
When working on a project, large or small, it is important to work to a set of guidelines to help keep stylesheets:

- Consistent
- Maintainable
- Readable
- Scalable

This means any number of developers can work within a stylesheet without the worry of disrupting the flow of development.


## Syntax and Formatting
### Fundamentals
In it's basic form a CSS ruleset should:

- Use four (4) space indents (no tabs)
- Use the 80 character wide column limit
- Use lowercase
- Have each selector on a new line
- Have the opening brace on the same line as the last selector
- Have a single space before the opening brace
- Have each declaration on a new line
- Have each declaration indented by four (4) spaces
- Have each declaration in alphabetical order
- Have no space before a property colon
- Have a single space after a property colon
- Have a trailing semi-colon at the end of each declaration
- Have the closing brace on a new line

```css
.selector-1,
.selector-2 {
    background-color: white;
    color: black;
}
```

### Extended
There are of course more than the basic selector, property/value declarations. To extend on the above rules they should:

- Use a single colon for pseudo classes
- Use a double colon for pseudo elements
- Use single quotes for strings, url values etc
- Have any decimal marked values include a zero (0)
- Have any comma separated values separated with a single space
- Have no padded spaces in parentheses

```css
.selector-1:first-child {
    background-image: url('/path/to/image.jpeg');
    color: hsla(0, 100%, 50%, 1);
    opacity: 0.5;
}
```

```css
.selector-1::before {
    content: 'I am a pseudo element!';
}
```

### Shorthand vs Longhand
Using shorthand or longhand is dependent on what property you wish to declare. For example, declaring each individual value of an elements' padding using individual longhand property doesn't make sense when you can declare it with one shorthand property.

**Good:**
```css
.selector {
    padding: 5px;
}
```

**Bad:**
```css
.selector {
    padding-bottom: 5px;
    padding-left: 5px;
    padding-right: 5px;
    padding-top: 5px;
}
```

The same goes for declaring each sides' padding in the shorthand property. Declaring each side should be avoided if all values are the same.

**Good:**
```css
.selector {
    padding: 5px;
}
```

**Bad:**
```css
.selector {
    padding: 5px 5px 5px 5px;
}
```

However, the shorthand/longhand rule is more dependant on the situation. For example, when declaring a background color it makes sense to use the longhand `background-color` over the shorthand `background`.

If we have previously declared a background image on our selector, like so:

```css
.selector {
    background-image: url('/path/to/image.jpeg');
}
```

We could potentially overwrite the previously declared background image if we are not careful, for example:

**Good:**
```css
.selector {
    background-color: hsla(0, 100%, 100%, 1);
}
```

**Bad:**
```css
.selector {
    background: hsla(0, 100%, 100%, 1);
}
```


### Multi-line Property Values
Some properties allow for multiple value declarations, such as box shadows. Since this can become quite messy, we can separate each value to a new line. Multi-line property values should:

- Have each value on a new line
- Have each value indented to the same level as the first value

```css
.selector {
    box-shadow: 5px 5px 10px 0 hsla(0, 100%, 0%, 0.2),
                -5px -5px 10px 0 hsla(0, 100%, 50%, 0.1);
}
```

There may also be times when you could declare shorthand values on multiple lines too. For example, if we are using SASS, we could have 4 variables that declare the radius of each corner of an element.

```css
.selector {
    border-radius: $border-top-left-radius
                   $border-top-right-radius
                   $border-bottom-right-radius
                   $border-bottom-left-radius;
}
```

### Vendor Prefixes
Browsers sometimes add prefixes to experimental or nonstandard CSS properties, try to avoid declaring these in your CSS as you should really be using [autoprefixer](https://github.com/postcss/autoprefixer) within your build tools such as [Gulp](http://gulpjs.com/), [Grunt](https://gruntjs.com/) or [Webpack](https://webpack.js.org/). Autoprefixer will automatically add vendor prefixes to experimental and nonstandard CSS properties.


## Naming Conventions
Naming conventions are also extremely important and we should always ensure that everything is consistent, meaningful and coherent.

#### File Names:
Files names should:

- Use lowercase
- Use hyphen delimiters
- Use the .css extension
    - Unless it is a CSS pre-processor file then use the correct template extension
- Include .min extension for minified stylesheets
- Have an underscore at the start of the file name for partials

```
reset.css
app.min.css
flex-box.scss
_partial.scss
```

### BEM
>"Block Element Modifier is a methodology that helps you to create reusable components and code sharing in front-end development"

**Block:** Standalone entity that is meaningful on its own.

**Element:** Part of a block, has no standalone meaning and semantically tied to its block.

**Modifier:** Flag on a block or element. Used to change appearance or behavior.

All class naming conventions should:

- Use lowercase
- Use BEM methodology and structuring
- Use hyphen delimiters

```css
.component-block {}
.component-block__element {}
.component-block--modifier {}
```

Following on with the BEM methodology and structuring, block element descendants should not chain their parent elements in their own name. Each block element is its' own element and each name should only contain one (1) set of double underscores `__` and one (1) set of double hyphens `--`.

```css
.block {}
.block__head {}
.block__heading {}
```

### Hooks
#### State Hooks
State hooks are modifier classes that declare an element or components state, they can be prefixed with either the `is-` or `has-` namespace depending on the state the element is in.

- A link may be in an active state: `is-active`
- An accordion item element may be in an expanded state: `is-expanded`
- A button element may be disabled: `is-disabled`
- A carousel element may have content loading: `is-loading`
- A slider element may have content loaded: `has-loaded`
- A input element may contain an error: `has-error`

#### JavaScript Hooks
JavaScript hooks are classes that are used to trigger a script, they contain no styling and must always be prefixed with the `js-` namespace and scoped to the component it is attached to and suffixed with the action it takes.

- A panel component that can be toggled: `js-panel-toggle`
- A panel component that can be removed: `js-panel-remove`
- A modal component that can be closed: `js-modal-close`
- A dropdown element that can be triggered: `js-dropdown-trigger`

### Modifiers

Modifier classes should always be declared using the [BEM](#bem) methodology and structuring, except for [size](#size-modifiers), [color](#color-modifiers) and [feedback](#feedback-modifiers) modifiers. These type of modifiers should be declared in a similar fashion to [state hooks](#state-hooks). The reason for declaring these like state hook modifiers rather than component/BEM modifiers is that these modifiers are universal and would appear throughout various elements and components, it keeps the naming conventions, consistent, structured and easily readable.

#### Size Modifiers
When declaring component and element size modifiers, we recommend using these naming conventions:

```css
.selector.is-micro {}
.selector.is-tiny {}
.selector.is-small {}
.selector.is-large {}
.selector.is-huge {}
.selector.is-mega {}
```

#### Color Modifiers
When declaring component and element color modifiers, we recommend using these naming conventions:

```css
.selector.is-charcoal {}
.selector.is-emerald {}
.selector.is-primary {}
.selector.is-secondary {}
```

#### Feedback Modifiers
Unlike [size modifiers](#size-modifiers) and [color modifiers](#color-modifiers), feedback modifiers should use the `has-` prefix. When declaring component and element feedback modifiers, we recommend using these naming conventions:

```css
.selector.has-info {}
.selector.has-success {}
.selector.has-warning {}
.selector.has-error {}
```

## SASS
Since we use SASS in all of our projects and given the popularity of SASS, we should always try our best to seamlessly place SASS within our CSS stylesheet while following the above guidelines.

### Variables
SASS variables do not need to follow that of the [BEM](#bem) methodology and structuring, but should:

- Use lowercase
- Use hyphen delimiters
- Be declared at the top of a stylesheet (exceptions include variables within loops etc)
- Be declared alphabetically
- Be prefixed with the component name they are attached to
- Have no space before the variable name colon
- Have a single space after the variable name colon
- Have a single space before a flag
- Have a trailing semi-colon at the end of the value

```scss
$component-background-color: hsla(0, 100%, 100%, 1);
$component-width: 500px !default;

.selector {
    background-color: $component-background-color;
    width: $component-width;
}
```

### Maps
Maps are very similar to SASS [variables](#variables) in their naming conventions and structuring, except they allow for key value pairs rather than a single value, they follow the same guidelines as variables, but should:

- Have the opening parentheses on the same line as the variable/map name
- Have a single space before the opening parentheses
- Have each declaration on a new line
- Use single quotes around the key properties
- Have no space before a key property colon
- Have a single space after a key property colon
- Have no trailing comma on the last key value pair
- Have the closing parentheses on a new line
- Have a trailing semi-colon after the closing parentheses

```scss
$colors: (
    'primary': hsla(0, 100%, 100%, 1),
    'secondary': hsla(0, 100%, 0%, 1)
) !default;
```

### Mixins and Functions
Like SASS [variables](#variables) and [maps](#maps), mixins and functions do not need to follow that of the [BEM](#bem) methodology and structuring either, but should:

- Use lowercase
- Use hyphen delimiters
- Have the argument parentheses on the same line as the mixin/function name
- Have no space before the opening parentheses
- Have no padded spaces in argument parentheses
- Have any comma separated argument values separated with a single space
- Have no space before an argument default value colon
- Have a single space after an argument default value colon
- Have the opening brace on the same line as the mixin/function
- Have a single space before the opening brace
- Have the closing brace on a new line

```scss
@mixin border-radius($top-left: 0, $top-right: 0, $bottom-right: 0, $bottom-left: 0) {
    // Mixin code...
}
```

```scss
@function set-font-color($background-color) {
    // Function code...
}
```

### Declaration Order
As mentioned above, we should always try our best to seamlessly place SASS within our CSS stylesheet. The declaration order of SASS and CSS should be as followed:

- Extend calls `@extend`
- Mixin calls `@include` (with no `@content`)
- CSS Declarations
- Pseudo classes
- Pseudo elements
- State hooks
- Size modifier hooks
- Color modifier hooks
- Feedback modifier hooks
- Modifiers
- Nested selectors
- Mixin calls `@include` (with `@content`)

```scss
.selector {
    @extend .element;
    @include border-radius(5px);
    background-color: hsla(0, 100%, 0%, 1);
    color: hsla(0, 100%, 100%, 1);

    &:first-child {}

    &::before {}

    &.is-active {}

    &.is-small {}

    &.is-primary {}

    &.has-error {}

    &.selector--modifier {}

    .selector__element {}

    @include breakpoint('mobile') {}
}
```

### Conditional Statements
SASS has the ability to calculate if/else conditional statements, they should:

- Have a single space before the opening parentheses
- Have no padded spaces in parentheses
- Have no space after a negation/NOT logical operator
- Have the opening brace on the same line
- Have a single space before the opening brace
- Have the closing brace on a new line
- Have the else key word on the same line as the closing and opening brace

```scss
@if (!$variable) {
    // Do something...
} @else {
    // Do something else...
}
```

### Partials
Since we can easily import files within our SASS stylesheets when we compile to CSS, we should always aim to break individual components and sections into their respective files and folders.


## Commenting
You may of noticed that none of the examples above have any form of comments in them, this is intended as to not clutter the examples shown. However, we should always ensure that our stylehsheets are well documented and should be aiming to:

- Break code into sections with headings within a single stylesheet if required
- Use DocBlocks, single line and inline comments for their correct purpose

### Headings
All of our stylesheets should include a heading or as mentioned above, individual headings to break code into sections within a single stylesheet, headings should:

- Have two (2) empty lines above
    - Unless it is the first heading of the stylesheet
- Open with one (1) forward slash, one (1) asterisk, two (2) spaces and ninety two (72) equals signs
    - Leaving 4 spaces at the end for the 80 character wide column limit
- Have the heading text on a new line
- Have four (4) spaces before the heading text
- Have capitalised heading text
- Use a breadcrumb pattern showing the partial/component directory architecture
- Use a hyphen and greater than sign for breadcrumb delimiters
- Have a space either side of breadcrumb delimiters
- Close on a new line
- Close with four (4) spaces, ninety two (72) equals signs, two (2) spaces, one (1) asterisk and one (1) forward slash
    - Using the 80 character wide column limit
- Have one (1) empty line below

```scss
/*  ========================================================================
    APPLICATION -> COMPONENTS -> NOTICE -> VARIABLES
    ========================================================================  */

$notice-background-color: hsla(0, 100%, 100%, 1);
$notice-border-width: 1px;
$notice-border-color: hsla(0, 100%, 100%, 1);
$notice-border-style: solid;


/*  ========================================================================
    APPLICATION -> COMPONENTS -> NOTICE
    ========================================================================  */

.notice {
    background-color: $notice-background-color:
    border: $notice-border-width
            $notice-border-style
            $notice-border-color;
    color: $notice-font-color;
}
```


### Inline
Inline comments are short and concise and should:

- Start on the same line as the subject matter
- Start with two (2) forward slashes
- Have a single space before the forward slashes
- Have a single space after the forward slashes
- Have a capitalised first letter
- Always be on one line
- Coherently explain what we are doing

```css
.selector {
    width: 100%; // Make the element responsive
}
```

For more on inline comments and what to do when multiple inline comments are repeated within a CSS ruleset or if the inline comment exceeds the 80 character wide column limit, read [number labels](#number-labels).

### DocBlocks
#### Basics
A DocBlock comment is used when a detailed description or explanation is needed, their format should:

- Open with one (1) forward slash and two (2) asterisk
- Have the first line of text on a new line
- Have each new line start with one (1) space, one (1) asterisk and two (2) spaces before the line of text
- Have each line of text wrap before the 80 character wide column limit
- Have a capitalised first letter for descriptions
- Have a full stop at the end of descriptions
- Close on a new line
- Close with one (1) space, one (1) single asterisk and one (1) forward slash

```css
/**
 *  Notice components should be used to showcase dismissible feedback to a user
 *  such as information, success, warning or error messages.
 */
.notice {}
```

#### Reference Subjects
DocBlocks can also include references to demos, authors and versions as well as crediting people. These are known as reference subjects with reference text and are declared with the following:

- `@demo`
- `@author`
- `@version`
- `@credit`

Reference subjects should:

- Have an empty line above the first reference subject
    - Unless it is the first line of a block
- Have each reference on a new line
- Have the first letter of the reference text inline with one another

```css
/**
 *  Notice component description.
 *  
 *  @demo    http://www.example.com/notice/demo
 *  @author  Joe Mottershaw <https://www.github.com/joemottershaw>
 *  @version 0.1.0
 */
.notice {}
```


#### SASS Annotations
DocBlocks can also include annotations for mixins and functions. These are known as SASS annotations with various types of annotation text structures depending on the annotation types. They follow the same structure as [reference subjects](#reference-subjects). Mixin and function annotations are:

**`@param`:**
```css
/**
 *  Function/mixin description.
 *  @param {type}  $parameter  The parameter description.
 */
```

**`@output`:**
```css
/**
 *  Mixin description.
 *  @output A output description.
 */
```

**`@return`:**
```css
/**
 *  Function description.
 *  @return {type}  The return description.
 */
```

When combining either of the SASS annotations, `{type}`, `$paramater` and the annotation description, they should:

- Have each annotation on a new line
- Have types aligned with one another
- Have parameters aligned with one another
- Have descriptions aligned with one another
- Have at least one (1) space between the annotation subject and type
- Have at least two (2) spaces between types and parameters
- Have at least two (2) spaces between parameters and descriptions
- Have a capitalised first letter for descriptions
- Have a full stop at the end of descriptions
- Use `{mixed}` for parameter types if multiple values are allowed
- Use `{mixed}` for return types if different values could be returned
- Use `{void}` for return types where nothing is returned

```scss
/**
 *  Mixin description.
 *  @param  {int}    $first   The first description.
 *  @param  {mixed}  $second  The second description.
 *  @output                   The output description.
 */
```

```scss
/**
 *  Function description.
 *  @param  {int}     $first   The first description.
 *  @param  {mixed}   $second  The second description.
 *  @return {string}           The return description.
 */
```

#### Number Labels
Number labels are used when [inline comments](#inline) would need to be repeated or if an inline comment exceeds the 80 character wide column limit. They should follow the same structure as inline comments and should also:

- Have the label wrapped in square brackets
- Have no padded spaces in square brackets

Use [DocBlocks](#docblocks) to declare each number and their respective comments, they should:

- Have an empty line above the first label
    - Unless it is the first line of a block
- Have each label start on a new line
- Use a number followed by a full stop
- Have one (1) space before the number label text
- Have a capitalised first letter for the number label text

```css
/**
 *  Some information about this ruleset.
 *  
 *  1. Make the element responsive
 *  2. Force the element to stack higher
 */
.selector {
    height: auto; // [1]
    width: 100%; // [1]
    z-index: 10; // [2]
}
```

You should never mix inline comments and number labels. Once a number label is used, convert all current inline comments for that ruleset to number labels to keep the stylesheet clean and consistent.

#### Ordering
Since there are many levels to a DocBlock depending on what the DocBlock is being used for, the above sections should be ordered as follows:

- [Basics](#basics)
- [SASS Annotations](#sass-annotations)
- [Number Labels](#number-labels)
- [Reference Subjects](#reference-subjects)

```scss
/**
 *  Mixin to make an element responsive and appear higher in the stack index.
 *  @param  {string}  $width   The element width.
 *  @param  {int}     $zindex  The z-index.
 *  @output                    The responsive property values.
 *
 *  1. Make the element responsive
 *  2. Force the element to stack higher
 *
 *  @demo    http://www.example.com/mixin/demo
 *  @author  Joe Mottershaw <https://www.github.com/joemottershaw>
 *  @version 0.1.0
 */
@mixin name($width, $zindex) {
    height: auto; // [1]
    width: $width; // [1]
    z-index: $zindex; // [2]
}
```


### Single Line
Single line comments are typically used above a declaration, set of variables or if/else statements etc. Single line comments should:

- Have an empty line above the comment
    - Unless it is the first line of a block
- Start with two (2) forward slashes
- Have a single space after the forward slashes
- Have a capitalised first letter
- Have the subject matter on a new line
- Coherently explain what we are doing

```scss
// Set the base colors
$color-black: hsla(0, 100%, 0%, 1);
$color-white: hsla(0, 100$, 100%, 1);

// Check if a variable is true
@if ($variable == true) {
    // Set the background color
    $background-color: $color-black;

    // Set the font color
    $font-color: $color-white;
} @else {
    // Set the background color
    $background-color: $color-white;

    // Set the font color
    $font-color: $color-black;
}
```


## Attributions
This CSS guideline is inspired *heavily* from [Chris Pearce](https://github.com/chris-pearce) and his [CSS Guidelines](https://github.com/chris-pearce/css-guidelines) which was "borrowed (shamelessly)" from [Harry Roberts](http://csswizardry.com/) and his [CSS Guidelines](http://cssguidelin.es/). Other notable sources are [Nicolas Gallagher](https://github.com/necolas) and his [Idiomatic CSS](https://github.com/necolas/idiomatic-css).
