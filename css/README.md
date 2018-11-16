# Style Guidelines: CSS
> *A set of guidelines to CSS.*

<br />



## Table of Contents
1. [Introduction](#introduction)
2. [Foundation](#foundation)
3. [Anatomy](#anatomy)
4. [Syntax and Formatting](#syntax-and-formatting)
    - [Fundamentals](#fundamentals)
    - [Extended](#extended)
    - [Shorthand vs Longhand](#shorthand-vs-longhand)
    - [Multi-line Property Values](#multi-line-property-values)
5. [Naming Conventions](#naming-conventions)
    - [BEM](#bem)
    - [State Hooks](#state-hooks)
    - [JavaScript Hooks](#javascript-hooks)
    - [Sizes](#sizes)
    - [Colors](#colors)
    - [Feedback](#feedback)
6. [SASS](#sass)
    - [Variables](#variables)
    - [Maps](#maps)
    - [Mixins and Functions](#mixins-and-functions)
    - [Declaration Order](#declaration-order)
    - [Conditional Statements](#conditional-statements)
    - [Partials](#partials)
7. [Commenting](#commenting)
    - [Headings](#headings)
    - [DocBlocks](#docblocks)
    - [Single Line](#single-line)
    - [Inline](#inline)
    - [Number Labels](#number-labels)
8. [Attributions](#attributions)


## Introduction
This is a style guideline for CSS that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to write CSS for your projects and we're always happy for insights, feedback, improvements and recommendations to help improve it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.


## Foundation
When working on projects, large or small, it is important to work to a set of guidelines to help keep stylesheets:

- Consistent
- Maintainable
- Readable
- Scalable

This means any number of developers can work within a stylesheet and have a good understanding of what they are working with and without the worry of disrupting the flow of development.


## Anatomy
```
[selector] {
    [property]: [value];
}
```

## Syntax and Formatting
### Fundamentals
Looking at the anatomy of a CSS ruleset above, these are the main fundamental rules they should:

- Use four (4) space indents (no tabs)
- Use 100 characters max
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
- Have a closing brace on a new line

**Good:**

```css
.selector-1,
.selector-2 {
    background-color: white;
    color: black;
}
```

**Bad:**
```css
.selector-1, .selector-2
{
    color:black;
    background-color : white;
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

**Good (Pseudo Class):**

```css
.selector-1:first-child {
    background-image: url('/path/to/image.jpeg');
    color: hsla(0, 100%, 50%, 1);
    opacity: 0.5;
}
```

**Bad (Pseudo Class):**

```css
.selector-1:first-child {
    background-image: url( "/path/to/image.jpeg" );
    color: hsla( 0,100%,50%,1 );
    opacity: .5;
}
```

**Good (Pseudo Element):**

```css
.selector-1::before {
    content: 'I am a pseudo element!';
}
```

**Bad (Pseudo Element):**

```css
.selector-1:before {
    content: "I am a pseudo element!";
}
```

### Shorthand vs Longhand
Using shorthand or longhand is dependant on what property you wish to declare. For example, declaring each individual value of an elements padding using each longhand property doesn't make sense when you can declare it with one shorthand property.

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

The same goes for declaring each sides' padding in the shorthand. Declaring each side should be avoided if all values are the same.

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

Basically, the shorthand/longhand rule is more dependant on the situation. For example, when declaring a background color it makes sense to use the longhand `background-color` over the shorthand `background`.

If we have previously declared a background image on our selector:

```css
.selector {
    background-image: url('/path/to/image.jpeg');
}
```

We could potentially overwrite the previously declared background image if we are not careful:

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
Some properties allow for multiple value declarations, such as box shadows. For multi-line values there are additional rules where the ruleset should:

- Have each value on a new line
- Have each value indented to the same level as the first value

**Good:**

```css
.selector {
    box-shadow: 5px 5px 10px 0 hsla(0, 100%, 0%, 0.2),
                -5px -5px 10px 0 hsla(0, 100%, 50%, 0.1);
}
```

**Bad:**

```css
.selector {
    box-shadow: 5px 5px 10px 0 hsla(0, 100%, 0%, 0.2), -5px -5px 10px 0 hsla(0, 100%, 50%, 0.1);
}

.selector {
    box-shadow: 5px 5px 10px 0 hsla(0, 100%, 0%, 0.2),
    -5px -5px 10px 0 hsla(0, 100%, 50%, 0.1);
}
```

There may also be times when it is more readable to declare shorthand values on multiple lines too. For example, if we have 4 variables that declare the radius of each corner of an element, we could declare them on multiple lines to make the stylesheet more coherent. This sort of practice also helps keep within our 100 character rule.

**Good:**

```css
.selector {
    border-radius: $border-top-left-radius
                   $border-top-right-radius
                   $border-bottom-right-radius
                   $border-bottom-left-radius;
}
```

**Bad:**

```css
.selector {
    border-radius: $border-top-left-radius $border-top-right-radius $border-bottom-right-radius $border-bottom-left-radius;
}
```


## Naming Conventions
Naming conventions are also extremely important and we should always ensure that classes and variable names are meaningful and coherent.

### BEM
>"Block Element Modifier is a methodology that helps you to create reusable components and code sharing in front-end development"

**Block:** Standalone entity that is meaningful on its own.

**Element:** Part of a block, has no standalone meaning and semantically tied to its block.

**Modifier:** Flag on a block or element. Used to change appearance or behavior.

All class naming conventions should:

- Use lowercase
- Use BEM methodology and structuring
- Use hyphen delimiters

**Good:**

```css
.card-block {}
.card-block--modifier {}
.card-block__element {}
```

**Bad:**

```css
.CardComponent {}
.CardComponent_Modifier {}
.CardComponent_Element {}
```

Following on with the BEM methodology and structuring, block element descendants should not chain their parent elements in their name. Each block element is its' own element and each name should only contain one (1) set of double underscores `__` and one (1) set of double hyphens `--`.

**Good:**

```css
.block {}
.block__head {}
.block__heading {}
```

**Bad:**

```css
.block {}
.block__head {}
.block__head__heading {}
```

### State Hooks
State hooks are modifier classes that declare an element or components state, they can be prefixed with either the `is-` or `has-` namespace depending on the state the element is in and the tense you would speak it:

- A link may be in an active state: `is-active`
- An accordion item element may be in an expanded state: `is-expanded`
- A button element may be disabled: `is-disabled`
- A carousel element may have content loading: `is-loading`
- A slider element may have content loaded: `has-loaded`
- A input element may contain an error: `has-error`

### JavaScript Hooks
JavaScript hooks are classes that are used to trigger a script, they contain no styling and must always be prefixed with the `js-` namespace and scoped to the component it is attached to and suffixed with the action it takes:

- A panel component that can be toggled: `js-panel-toggle`
- A panel component that can be removed: `js-panel-remove`
- A modal component that can be closed: `js-modal-close`
- A dropdown element that can be triggered: `js-dropdown-trigger`

### Sizes
When declaring size modifier classes, along with the default declarations you may wish to decrease or increase the property values, try and stick to these naming conventions for sizing components and elements:

- Tiny
- Small
- Large
- Huge

However, there may be cases where components and elements need even smaller or bigger styles, if so you can use the following:

- Micro
- Mega

Use these naming conventions as state hook modifiers like so:

```css
.selector.is-micro {}
.selector.is-tiny {}
.selector.is-small {}
.selector.is-large {}
.selector.is-huge {}
.selector.is-mega {}
```

The reason for declaring them as state hook modifiers rather than BEM modifiers is these modifiers are universal and would appear throughout various elements and components, it keeps the naming conventions structured and easily readable.

### Colors
Similar to sizes, use these modifier classes as state hook modifiers too, this can include base colors, primary and secondary colors, for example:

```css
.selector.is-charcoal {}
.selector.is-emerald {}
.selector.is-primary {}
.selector.is-secondary {}
```

### Feedback
Feedback naming conventions include:

- Info
- Success
- Warning
- Error

Just like colors, use these modifier classes as state hook modifiers but with the `has-` prefix, like so:

```css
.selector.has-info {}
.selector.has-success {}
.selector.has-warning {}
.selector.has-error {}
```



## SASS
Since we use SASS in all of our projects and given the popularity of SASS, there are guidelines that we wish to include in our CSS guidelines, without trying to showcase the functionality or features of SASS, here is how we best place SASS in our CSS in the most compatible way, following the above guidelines.

### Variables
SASS variables do not need to follow that of the BEM methodology and structuring, but should:

- Use lowercase
- Use hyphen delimiters
- Be declared alphabetically
- Be declared at the top of a stylesheet (exceptions include variables within loops etc)
- Be prefixed with the component name they are attached to
- Have no space before the variable name colon
- Have a single space after the variable name colon
- Have a trailing semi-colon at the end of the value

**Good:**

```scss
$component-background-color: hsla(0, 100%, 100%, 1);
$component-width: 500px;

.selector {
    background-color: $component-background-color;
    width: $component-width;
}
```

**Bad:**

```scss
.selector {
    $ComponentWidth : 500px;
    $ComponentBackgroundColor:hsla(0, 100%, 100%, 1);

    background-color: $ComponentBackgroundColor;
    width: $ComponentWidth;
}
```

### Maps
Maps are very similar to variables in their naming conventions and structuring, except they allow for key value pairs rather than a single value, they should follow everything mentioned in the SASS [variables](#variables), but should:

- Have the opening parentheses on the same line as the variable/map name
- Have a single space before the opening parentheses
- Have each declaration on a new line
- Use lowercase for key property names
- Have key properties wrapped in single quotes
- Have no space before a key property colon
- Use single space after a key property colon
- Have no trailing comma on the last key value pair
- Have the closing parentheses on a new line
- Have a trailing semi-colon after the closing parentheses

**Good:**

```scss
$colors: (
    'primary': hsla(0, 100%, 100%, 1),
    'secondary': hsla(0, 100%, 0%, 1)
);
```

**Bad:**
```scss
$colors:
(
    primary:hsla(0, 100%, 100%, 1),
    secondary : hsla(0, 100%, 0%, 1),
);
```

### Mixins and Functions
Like SASS variables, mixins and functions do not need to follow that of the BEM methodology and structuring, but should:

- Use lowercase
- Use hyphen delimiters
- Have the argument parentheses on the same line as the mixin name
- Have no space before the opening parentheses
- Have no padded spaces in argument parentheses
- Have any comma separated argument values separated with a single space
- Have no space before an argument default value colon
- Have a single space after an argument default value colon
- Have the opening brace on the same line as the mixin name and argument parentheses parentheses
- Have a single space before the opening brace
- Have the closing brace on a new line

**Good (Mixin):**

```scss
@mixin border-radius($top-left: 0, $top-right: 0, $bottom-right: 0, $bottom-left: 0) {
    border-radius: $top-left
                   $top-right
                   $bottom-right
                   $bottom-left;
}
```

**Bad (Mixin):**

```scss
@mixin BorderRadius( $top-left:0, $top-right:0, $bottom-right:0, $bottom-left:0 )
{
    border-radius:$top-left $top-right $bottom-right $bottom-left;
}
```

**Good (Function):**

```scss
@function set-font-color($background-color) {
    // Function code...
}
```

**Bad (Function):**

```scss
@function setFontColor( $background-color )
{
    // Function code...
}
```

### Declaration Order
As mentioned above, here is how we best place SASS in our CSS in the most compatible way, the declaration order of SASS and CSS should be as followed:

- Extend calls `@extend`
- Mixin calls `@include` (with no `@content`)
- CSS Declarations
- Pseudo classes
- Pseudo elements
- State hooks
- Modifiers
- Nested selectors
- Mixin calls `@include` (with `@content`)

**Good:**

```scss
.selector {
    @extend .element;
    @include border-radius(5px);
    background-color: hsla(0, 100%, 0%, 1);
    color: hsla(0, 100%, 100%, 1);

    &:first-child {}

    &::before {}

    &.is-active {}

    &.selector--modifier {}

    .selector__element {}
}
```

**Bad:**

```scss
.selector {
    @include border-radius(5px);
    color: hsla(0, 100%, 100%, 1);
    background-color: hsla(0, 100%, 0%, 1);
    @extend .element;

    .selector__element {}

    &::before {}

    &:first-child {}

    &.selector--modifier {}

    &.is-active {}
}
```

### Conditional Statements
SASS has the ability to calculate if/else conditional statements, they should:

- Have a single space before the opening parentheses
- Have no padded spaces in parentheses
- Have the opening/extending else brace on the same line as the if/else keywords
- Have the closing brace on a new line

**Good:**

```scss
@if ($variable == true) {
    // Do something...
} @else {
    // Do something else...
}
```

**Bad:**

```scss
@if( $variable == true )
{
    // Do something...
}
@else
{
    // Do something else...
}
```

### Partials
Since we can easily import files within our SASS stylesheets when we compile to CSS, we should always aim to break individual components and sections into their respective files and folders. This helps keep our code separated and easily maintained.


## Commenting
You may of noticed that none of the examples above have any form of comments in them, this is intended as to not clutter the examples shown. However, we should always ensure that our files are well documented and should be aiming to:

- Break code into sections with headings within a single stylesheet
- Use DocBlocks, single line and inline comments for their correct purpose


### Headings
All of our stylesheets should include a heading or as mentioned above, individual headings to break code into sections within a single stylesheet, headings should:

- Have two (2) empty lines above
    - Unless it is the first heading of the stylesheet
- Open with one (1) forward slash followed by one (1) asterisk
- Have the heading text on a new line
- Have capitalised heading text
- Use a breadcrumb pattern showing the partial architecture
- Use a hyphen and greater than sign as the breadcrumb
- Close with one (1) asterisk followed by one (1) forward slash
- Have a repeated equals sign fill above and below the heading text on the opening and closing lines
- Have the heading text inline with the first equals symbols
- Have one (1) empty line below

**Example:**

```scss
/* =============================================================================================
   APPLICATION -> COMPONENTS -> NOTICE -> VARIABLES
   ============================================================================================= */

$notice-background-color: hsla(0, 100%, 100%, 1);
$notice-border-bottom-width: 3px;
$notice-border-left-width: 1px;
$notice-border-right-width: 1px;
$notice-border-top-width: 1px;
$notice-border-color: hsla(0, 100%, 100%, 1);
$notice-border-style: solid;


/* =============================================================================================
   APPLICATION -> COMPONENTS -> NOTICE
   ============================================================================================= */

.notice {
	background-color: $notice-background-color:
	border: 0 $notice-border-style $notice-border-color;
	border-bottom-width: $notice-border-bottom-width;
	border-left-width: $notice-border-left-width;
	border-right-width: $notice-border-right-width;
	border-right-width: $notice-border-top-width;
	color: $notice-font-color;
}
```


### DocBlocks
A DocBlock comment is used when a detailed description or explanation is needed, their format should:

- Open with one (1) forward slash followed by two (2) asterisk
- Have the first line of text on a new line
- Have a single space before each new line
- Have each new line start with one (1) asterisk
- Have a single space before a line of text
- Close on a new line
- Close with one (1) single asterisk followed by one (1) forward slash

**Good:**

```css
/**
 * Notice components should be used to showcase dismissable feedback to a user
 * such as information, success, warning or error messages.
 */
```

**Bad:**

```css
/* Notice components should be used to showcase dismissable feedback to a user
* such as information, success, warning or error messages. */
```

DocBlocks can also include references to demos, authors as well as crediting people. These are known as reference subjects and are declared with the following:

- `@demo`
- `@author`
- `@version`
- `@credit`
- `@markup`

References should always be declared at the end of the DocBlock, they should:

- Have an empty line above
    - Unless it is the first line of a block
    - Or if a reference subject/text is above it
- Have the first letter of the reference text inline with one another

**Good:**

```css
/**
 * Notice component text...
 *
 * @author  Joe Mottershaw <https://www.github.com/joemottershaw>
 * @version 0.1.0
 */
.notice {
	.notice__text {}
	.notice__remove {}
}
```

**Bad:**

```css
/**
 * Notice component text...
 * @author Joe Mottershaw <https://www.github.com/joemottershaw>
 * @version 0.1.0
 */

.notice {
	.notice__text {}
	.notice__remove {}
}
```

However, the `@markup` reference should always be placed last as this breaks the format of the DocBlock and doesn't include an asterisk on each new line as it contains information that would be selected to be copied.

`@markup` references should be declared like this:

```css
/**
 * Notice component text...
 *
 * @author  Joe Mottershaw <https://www.github.com/joemottershaw>
 * @version 0.1.0
 * @markup
    <div class="notice">
        <div class="notice__text">
            [text]
        </div>
        <div class="notice__remove js-notice-remove">
           [remove_icon]
        </div>
    </div>
 */
```

### Single Line
Single line comments are typically used above a declaration, set of variables or if/else statements etc. Single line comments should:

- Have an empty line above
    - Unless it is the first line of a block
- Start with two (2) forward slashes
- Have a single space after the forward slashes
- Have a capitalised first letter
- Have the subject matter on a new line
- Coherently explain what we are doing

**Good:**

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

**Bad:**

```scss
// Colors

$color-black: hsla(0, 100%, 0%, 1);
$color-white: hsla(0, 100$, 100%, 1);


// Check if a variable is true
@if ($variable == true) {
    // Background
    $background-color: $color-black;
    // Font color
    $font-color: $color-white;
} @else {

    // Background
    $background-color: $color-white;
    // Font color
    $font-color: $color-black;

}
```

### Inline
Inline comments should be used after things such as a CSS property value declarations, they should be short and concise and should:

- Start on the same line as the subject matter
- Start with two (2) forward slashes
- Have a single space after the forward slashes
- Have a capitalised first letter
- Always be on one line
- Coherently explain what we are doing

**Good:**
```css
.selector {
	width: 100%; // Make the element responsive
}
```

**Bad:**
```css
.selector {
	width: 100%;//responsive
}
```


### Number Labels

Number labels are used when inline comments would need to be repeated or if an inline comment surpassed the 100 character limit. They should follow the same structure as inline comments and should also:

- Have the label wrapped in square brackets
- Have no padded spaces in square brackets

Use DocBlocks to declare each number and their respective comments, they should:

- Have an empty line above first label
    - Unless it is the first line of a block
- Have the first letter of the label text inline with one another

**Good:**

```css
/**
 * Some information about this ruleset
 *
 * 1.  Make the element responsive
 * 2.  Force the element to stack higher
 * ...
 * 10. Remove any webkit styling
 */
.selector {
    -webkit-appearance: none; // [10]
    height: auto; // [1]
    width: 100%; // [1]
    z-index: 10; // [2]
}
```

**Bad:**

```css
/**
 * Some information about this ruleset
 * 1. Make the element responsive
 * 2. Force the element to stack higher
 * ...
 * 10. Remove any webkit styling
 */
.selector {
    -webkit-appearance: none; // [10]
    height: auto; // [1]
    width: 100%; // [1]
}
```

You should never mix inline and number labels, once a number label is used, convert all current inline comments to number labels to keep the stylesheet clean and consistent.


## Attributions
This CSS guideline is inspired *heavily* from [Chris Pearce](https://github.com/chris-pearce) and his [CSS Guidelines](https://github.com/chris-pearce/css-guidelines) which was "borrowed (shamelessly)" from [Harry Roberts](http://csswizardry.com/) and his [CSS Guidelines](http://cssguidelin.es/). Other notable sources are [Nicolas Gallagher](https://github.com/necolas) and his [Idiomatic CSS](https://github.com/necolas/idiomatic-css).
