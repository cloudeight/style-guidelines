# Style Guidelines: HTML and Templates
> *A set of guidelines to HTML and templates.*
<br />


## Table of Contents
1. [Introduction](#introduction)
2. [HTML](#html)
    - [Fundamentals](#fundamentals)
    - [Doctype](#doctype)
    - [Language](#language)
    - [Character Encoding](#character-encoding)
    - [Viewport](#viewport)
    - [Closing Elements](#closing-elements)
    - [Attributes](#attributes)
        - [Basics](#basics)
        - [Ordering](#ordering)
        - [Boolean Flags](#boolean-flags)
        - [Images](#images)
    - [Stylesheets and Scripts](#stylesheets-and-scripts)
3. [Templates](#templates)
    - [Variables](#variables)
        - [Output](#output)
        - [Filters](#filters)
    - [Functions](#functions)
    - [Expressions](#expressions)
    - [Naming Conventions](#naming-conventions)
	    - [Variables](#variables-1)
	    - [Filters](#filters-1)
	    - [Functions](#functions-1)
	    - [File Names](#file-names)
	    - [Exceptions](#exceptions)
4. [Comments](#comments)
    - [Single Line](#single-line)
    - [Multi-line](#multi-line)
    - [Inline](#inline)
    - [Template Equivalents](#template-equivalents)


## Introduction
This is a style guideline for HTML and templates that we use for projects at [cloudeight](https://github.com/cloudeight/) as part of our [style guidelines](https://github.com/cloudeight/style-guidelines) documentation project.

It is in no way perfect or the definitively correct way to write changelogs for your projects and we're always happy for insights, feedback, improvements and recommendations to help improve it!

Some projects written before this guideline may not follow it entirely or at all and there may be times when projects follow their own guidelines due to special use cases. Of course, these guidelines may be updated as and when needed.

## HTML
### Fundamentals
For consistency between HTML documents, you should:

- Use four (4) space indents (no tabs)
- Use the 100 character wide column limit
- Use lowercase
- Have an empty line above each new line element tag
    - Unless it is the first new line element tag of a section
- Have no empty line below the last element tag of a section

```html
<article>
    <h1>Heading</h1>

    <p>Lorem ipsum dolor sit amet...</p>

    <button>Continue</button>
</article>
```

### Doctype
Always enforce standards mode so that the browser will know the expected document type. It should be the first declaration of your document.

```html
<!doctype html>
<html>
    <head>
    </head>

    <body>
    </body>
</html>
```

### Language
> *Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.*

```html
<html lang="en">
</html>
```

For a list of accepted language codes, take a look at the [ISO 2 Letter Language Codes](https://www.sitepoint.com/iso-2-letter-language-codes/) article on SitePoint.

### Character Encoding
Always declare the character set in each of your HTML documents, this ensures correct rendering of your content.

```html
<head>
    <meta charset="utf-8">
</head>
```

### Viewport
In most of our projects we tend to use the same viewport settings, however, some projects will obviously require different needs, but for the majority of our projects we use:

```html
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
```

This tells the browser that the website should adapt to the device width while setting the initial zoom/scale. It also tells the browser that the viewer cannot zoom in or out of the page. The reason for this is we should be using responsive web design with media queries to adapt our sites to the device being used. Obviously this can be adjusted on a per project basis but is a good starting point.

### Closing Elements
There are 2 types of element tags, container elements and non container elements. Container elements are element tags such as `<div></div>` and `<p></p>`, these are elements that can have nested elements within them. Non container elements are singular elements with no nested elements such as `<meta />` and `<input />`.

Always remember to:

- Close all container element tags with their respective closing tag
- Close all non container element tags with a self closing forward slash
- Have a space before the self closing forward slash

```html
<p>Lorem ipsum dolor sit amet...</p>

<meta />
```

### Attributes
#### Basics
Attributes vary from each element but the format of them should be consistent. Attributes should:

- Use lowercase
- Have no space between the attribute name, equals sign and attribute value
- Use double quotes for attribute values
- Have any comma separated values separated with a single space

```html
<a href="/path/to/file.html" target="_self">This is a link.</a>

<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```

#### Ordering
There are many attributes for various elements, focusing on *some* of the most commonly used attributes (more below), they should be declared in this order:

- `id`
- `class`
- `name`
- `value`
- `placeholder`
- `title`
- `alt`
- `role`
- `data-*`
- `aria-*`

However, there are other commonly used attributes which break this rule, the reason for this is they usually help declare a purpose to a particular element which is important and should take precedence for readability. These should be placed as the initial attributes of an element in the order that makes the most sense. These attributes are:

- `action`
- `for`
- `href`
- `method`
- `rel`
- `src`
- `type`

Any other elements' attributes should be placed in alphabetical order at the end of the attribute list.

#### Boolean Flags
Boolean attribute flags are attributes such as `disabled`, `checked` and `selected`. They should:

- Be declared as the last set of attributes of an element
- Be declared in alphabetical order
- Have no value attached to them

```html
<input type="text" disabled />

<input type="checkbox" value="1" checked />

<select>
    <option value="1" selected>1</option>
</select>
```

#### Images
Image elements should always have the alt attribute assigned to them.

```html
<img src="/path/to/image.jpeg" alt="Images description..." />
```

### Stylesheets and Scripts
When including stylesheets and scripts, with HTML5 there is no need to specify a type for either include. Also remember to use the [attribute ordering](#ordering) when declaring include attributes.

```html
<link rel="stylesheet" href="/path/to/reset.css">
<link rel="stylesheet" href="/path/to/stylesheet.css">

<script src="/path/to/script.js"></script>
```


## Templates
There are many template engines available, each having their own pro's and con's depending on your preferences. However, here at [cloudeight](https://github.com/cloudeight) we predominantly use [Twig](https://twig.symfony.com/) ([Symfony](https://symfony.com/)) in our own in house PHP MVC framework as well as [Timber](https://www.upstatement.com/timber/) for our WordPress projects. However, the main principles should apply to most other template engines such as the [Blade](https://laravel.com/docs/blade) or [Smarty](https://www.smarty.net/).

### Variables
Variables allow us to output data from a controller in an MVC architecture or set variables within the template itself.

#### Output
Variables in their basic form, as mentioned above, output data, they should:

- Have a single space after the opening output tag
- Use dot notation for both objects and arrays
- Have a single space before the closing output tag

```twig
{{ var }}
{{ var.foo }}
```

Refer to our [variable naming conventions](#variables-1) for more on naming your variables.

#### Filters
Filters allow us to manipulate and format the output of a variable, they should:

- Have no space before the pipe symbol
- Have no space after the pipe symbol
- Have no space before the argument parentheses
- Have no padded spaces in the argument parentheses
- Have any comma separated argument values separated with a single space
- Use single quotes for filter argument values

```twig
{{ var|striptags }}
{{ var|round(1, 'floor') }}
```

There maybe cases where an array of data can be passed to a filter, when this situation occurs, declaring the array as it's own variable/property using the `set` expression is preferred for better readability and clarity within the document. If that is the case, read the [expressions](#expressions) sections to understand how to correctly format expressions and then use the following example to place the variable property as an array in the filter argument.

```twig
{%
    set array = {
        '%this%': foo,
        '%that%': 'bar'
    }
%}

{{ "I like %this% and %that%."|replace(array) }}
```

Refer to our [filter naming conventions](#variables-2) for more on naming your custom filters.

### Functions
Functions can be used to generate content, they should:

- Have the argument parentheses on the same line as the function name
- Have no space before the opening parentheses
- Have no padded spaces in argument parentheses
- Have any comma separated arguments separated with a single space

```twig
{% if date(user.created_at) < date('-2days', 'Europe/London') %}
    {# Do something... #}
{% endif %}
```

Refer to our [function naming conventions](#functions-2) for more on naming your custom functions.

### Expressions
Expression tags allow us to set variables, loop through arrays and test conditionals. They should:

- Use lowercase
- Have each expression on a new line
- Have a single space after the opening expression tag
- Have a single space before the closing expression tag

When setting and declaring variables:

- Use single quotes for variable values
    - Unless the variable value is taking the value of another variable

```twig
{% set var = 'foo' %}
```

If an expression requires multiple lines then they should:

- Have the opening expression tag on its own line
- Have the expression indented four (4) spaces
- Split expression keywords to new lines where necessary (includes with passed data for example)
- Have the closing expression tag on its own line


If you are setting variable properties as arrays or objects or passing arrays to an include, they should:

- Have the opening array/object literal on the same line as the first line of the expression
- Use single quotes for key properties
- Have no space before a key property colon
- Have a single space after a key property colon
- Use single quotes for key values
    - Unless the key value is taking the value of another variable
- Have no trailing comma on the last key value pair
- Have the closing array/object literal on a new line

```twig
{%
    set var = {
        'foo': 'bar',
        'bar': 'baz'
    }
%}

{%
    include 'path/to/partial.twig'
    ignore missing
    with {
       foo: var.foo,
       bar: var.bar
    }
%}
```

When using control structures like if statements and for loops, they should:

- Have a single space after the opening expression tag
- Have a single space before the closing expression tag
- Have each expression keyword on a new line
- Have content indented four (4) spaces

```twig
{% if auth and user.role == 'subscriber' %}
    <h1>Welcome!</h1>

	<p>Content is visible...</p>
{% else %}
    <h1>Subscribe today!</h1>

	<p>Content is hidden...</p>
{% endif %}

{% if var == 'foo' %}
    {% set class = 'is-foo' %}
{% else %}
    {% set class = 'is-not-foo' %}
{% endif %}

<div class="block {{ class }}"></div>

{% for user in users %}
    <p>{{ user.name }}</p>
{% endfor %}
```

### Naming Conventions
Naming conventions are also extremely important and we should always ensure that variables, filters and function names are, consistent, meaningful and coherent.

#### Variables
When naming our variables we tend to use snake_case:

```twig
{% set custom_variable = 'foo' %}
```

#### Filters
When naming our custom filters we tend to use snake_case:

```twig
{{ var|custom_filter('type', 'data') }}
```

#### Functions
When naming our custom functions we tend to use snake_case:

```twig
{{ custom_function('type', 'data') }}
```

#### File Names:
Files names should:

- Use lowercase
- Use hyphen delimiters
- Use .html extension
	- Unless it is a template file then use the correct extension (.twig, .blade.php etc)
- Have an underscore at the start of the file name for partials

#### Exceptions
These naming conventions for variables, filters and function names follow the same naming conventions that Twig use. If you are using a different template engine that predominantly uses camelCase for function names for example then try and be consistent with the framework or engine you are using.

Also, take a look at the project you are contributing to, see what naming conventions are being used, ask an already contributing developer for advice, the main point is to be consistent.


## Comments
You may of noticed that none of the examples above have any form of comments in them, this is intended as to not clutter the examples shown. However, we should always ensure that our HTML files are well documented and should be aiming to:

- Use single line, multi-line and inline comments for their correct purpose

### Single Line
Single line comments are typically used above an element or template tag/expression. Single line comments should:

- Have an empty line above the comment
    - Unless it is the first line of a block
- Have a single space after the opening comment tag
- Have a capitalised first letter
- Have a single space before the closing comment tag
- Have the subject matter on a new line

```twig
<!-- This is a comment -->
<p>Lorem ipsum dolor sit amet...</p>

{# This is another comment #}
{{ var }}
```


### Multi-line
If a comment requires multiple lines, they should:

- Have an empty line above the comment
    - Unless it is the first line of a block
- Have the opening comment tag on its own line
- Have the comment text on a new line
- Have the comment text indented four (4) spaces
- Have each comment text line aligned to the first comment text line
- Have a capitalised first letter
- Have a full stop at the end of the comment
- Have the closing comment tag on its own line
- Have the subject matter on a new line

```twig
<!--
    This is a comment that requires multiple lines. It is more informative and
    descriptive than a single line comment.
-->
<p>Lorem ipsum dolor sit amet...</p>

{#
    This is a another comment that requires multiple lines. It is more informative and
    descriptive than a single line comment.
#}
{% for user in users %}
    <p>{{ user.name }}</p>
{% endfor %}
```

### Inline
Inline comments should be avoided and [single line](#single-line) and [multi-line](#multi-line) comments are preferred. For reference, here is an example of an inline comment:

```twig
<p>Lorem ipsum dolor sit amet...</p> <!-- This is an inline comment -->

{{ var }} {# This is a inline comment #}
```

There is a case where inline comments are used, when showcasing a closing tag and what tag it refers to.

```twig
<div class="container">
    <div class="grid">
	    {% for user in users %}
            <div class="grid__item">{{ user.name }}</div>
        {% endfor %} {# user loop #}
    </div> <!-- Grid -->
</div> <!-- Container -->
```

However, try to avoid them as if you have followed this style guideline it should remove the need for them. Elements should be nested correctly and with most modern text editors having collapsible sections as well as markup errors, it should be easy to see what each closing element corresponds to or if a tag is missing/incorrect.

### Template Equivalents
When using a template engine, they often have their own opening and closing comment tags, it is preferable to use these over the standard HTML opening and closing comment tags. As mentioned in the [templates](#templates) section, there are many template engines out there, but sticking to our initial statement of focusing primarily on [Twig](https://twig.symfony.com/), here is an example of how to replace traditional HTML comments tags with the template equivalents:

**Twig:**
```twig
<!-- This is a HTML comment -->
{# This is a Twig comment #}
```
