# SCSS-Notes

SCSS (Sassy CSS) is an extension of CSS that adds powerful features to enhance the development process. Here are various keywords and constructs commonly used in SCSS: 

  

### 1. Variables 

Variables allow you to store values and reuse them throughout your stylesheet. 

```scss 

$primary-color: #3498db; 

$font-stack: Helvetica, sans-serif; 

  

body { 

  font: 100% $font-stack; 

  color: $primary-color; 

} 

``` 

  

### 2. Nesting 

Nesting allows you to nest your CSS selectors in a way that follows the same visual hierarchy of your HTML. 

```scss 

nav { 

  ul { 

    margin: 0; 

    padding: 0; 

    list-style: none; 

  } 

  

  li { display: inline-block; } 

  

  a { 

    text-decoration: none; 

    color: $primary-color; 

  

    &:hover { 

      color: darken($primary-color, 10%); 

    } 

  } 

} 

``` 

  

### 3. Partials 

Partials allow you to create small SCSS files that can be included in other SCSS files. Partials are prefixed with an underscore (`_`). 

```scss 

// _reset.scss 

* { 

  margin: 0; 

  padding: 0; 

  box-sizing: border-box; 

} 

  

// main.scss 

@import 'reset'; 

``` 

  

 

 

### 4. Import 

The `@import` keyword allows you to include the content of one SCSS file in another. 

```scss 

@import 'reset'; 

@import 'variables'; 

@import 'mixins'; 

@import 'base'; 

``` 

  

### 5. Mixins 

Mixins allow you to create reusable chunks of CSS. 

```scss 

@mixin border-radius($radius) { 

  -webkit-border-radius: $radius; 

     -moz-border-radius: $radius; 

          border-radius: $radius; 

} 

  

.box { @include border-radius(10px); } 

``` 

  

### 6. Extend/Inheritance 

The `@extend` directive lets you share a set of CSS properties from one selector to another. 

```scss 

%message-shared { 

  border: 1px solid #ccc; 

  padding: 10px; 

  color: #333; 

} 

  

.message { @extend %message-shared; } 

.success { @extend %message-shared; background-color: #e0ffe0; } 

.error { @extend %message-shared; background-color: #ffe0e0; } 

``` 

  

### 7. Functions 

Functions allow you to define complex calculations and return values. 

```scss 

@function calculate-rem($size, $base: 16px) { 

  @return $size / $base * 1rem; 

} 

  

body { 

  font-size: calculate-rem(18px); 

} 

``` 

  

### 8. Control Directives and Expressions 

SCSS includes control directives such as `@if`, `@for`, `@each`, and `@while` for control flow. 

```scss 

// @if 

@mixin theme-colors($theme) { 

  @if $theme == dark { 

    background-color: black; 

    color: white; 

  } @else if $theme == light { 

    background-color: white; 

    color: black; 

  } @else { 

    background-color: gray; 

    color: black; 

  } 

} 

  

// @for 

@for $i from 1 through 3 { 

  .col-#{$i} { width: 100% / 3 * $i; } 

} 

  

// @each 

$themes: (primary: #3498db, secondary: #2ecc71, danger: #e74c3c); 

@each $name, $color in $themes { 

  .button-#{$name} { background-color: $color; } 

} 

  

// @while 

$i: 1; 

@while $i < 4 { 

  .item-#{$i} { width: 2em * $i; } 

  $i: $i + 1; 

} 

``` 

  

 

### 9. Placeholder Selectors 

Placeholder selectors (starting with `%`) are used with `@extend` but don’t output CSS on their own. 

```scss 

%hidden { 

  display: none; 

} 

  

.hidden-element { @extend %hidden; } 

``` 

  

### 10. Interpolation 

Interpolation is used to include variables in selectors and property names. 

```scss 

$side: left; 

.#{$side}-column { 

  float: $side; 

} 

``` 

  

### 11. Built-in Functions 

SCSS provides a wide range of built-in functions for manipulating colors, numbers, strings, and more. 

```scss 

$color: lighten(#3498db, 20%); // Lightens the color by 20% 

$width: 50px + 20px;           // Outputs 70px 

$quote: quote("Hello");        // Outputs "Hello" 

``` 

  

These features make SCSS a powerful preprocessor, allowing for more maintainable, reusable, and flexible stylesheets. 

 

 

In SCSS, placeholder selectors are special types of selectors that start with a `%` symbol. These selectors are designed to be used with the `@extend` directive, and they help to share sets of CSS rules among multiple selectors without generating any CSS on their own unless extended.  

  

  

In SCSS, placeholder selectors are special types of selectors that start with a `%` symbol. These selectors are designed to be used with the `@extend` directive, and they help to share sets of CSS rules among multiple selectors without generating any CSS on their own unless extended. 

### Placeholder Selector in detail

1. **Placeholder Selector Definition**:
   - A placeholder selector is defined using the `%` symbol followed by a name. 
   - Example:
     ```scss
     %button-base {
       padding: 10px 20px;
       border: none;
       border-radius: 5px;
       font-size: 16px;
     }
     ```

2. **Using `@extend`**:
   - The `@extend` directive is used within a selector to apply the styles of the placeholder selector.
   - Example:
     ```scss
     .btn-primary {
       @extend %button-base;
       background-color: blue;
       color: white;
     }

     .btn-secondary {
       @extend %button-base;
       background-color: gray;
       color: black;
     }
     ```

3. **Resulting CSS**:
   - The placeholder selector `%button-base` itself does not generate any CSS.
   - The `@extend` directive in `.btn-primary` and `.btn-secondary` copies the styles from `%button-base` into those selectors.
   - Compiled CSS:
     ```css
     .btn-primary, .btn-secondary {
       padding: 10px 20px;
       border: none;
       border-radius: 5px;
       font-size: 16px;
     }

     .btn-primary {
       background-color: blue;
       color: white;
     }

     .btn-secondary {
       background-color: gray;
       color: black;
     }
     ```

### Advantages of Using Placeholder Selectors

1. **DRY Principle (Don't Repeat Yourself)**:
   - Placeholder selectors help in reducing code duplication by allowing shared styles to be defined once and reused.

2. **Efficient CSS**:
   - Since placeholder selectors do not generate any CSS by themselves, they help keep the compiled CSS clean and efficient.

3. **Modular and Maintainable**:
   - Using placeholder selectors makes the SCSS code modular and easier to maintain. Changes to the shared styles need to be made only in one place.

### Summary
Placeholder selectors in SCSS are a powerful feature for sharing CSS rules among multiple selectors without directly outputting any CSS. They are used in combination with the `@extend` directive to apply the shared styles to other selectors, promoting code reusability, efficiency, and maintainability.


### Detailed Explanation of `@each`

The `@each` directive in SCSS is a powerful control structure that allows you to iterate over lists or maps and apply styles dynamically based on the values within these collections. It is particularly useful for generating repetitive styles efficiently and maintaining a DRY (Don't Repeat Yourself) codebase.


#### Syntax

The basic syntax for `@each` is:
```scss
@each $variable in $list {
  // Styles using $variable
}
```

### Iterating Over Lists

When iterating over a list, `@each` takes each item in the list and performs the specified block of styles.

#### Example with a List

```scss
$colors: red, green, blue;

@each $color in $colors {
  .text-#{$color} {
    color: $color;
  }
}
```

#### Resulting CSS

```css
.text-red {
  color: red;
}

.text-green {
  color: green;
}

.text-blue {
  color: blue;
}
```

### Iterating Over Maps

When iterating over a map, `@each` can destructure the key-value pairs and apply styles accordingly.

#### Example with a Map

```scss
$theme-colors: (
  primary: #3498db,
  secondary: #2ecc71,
  danger: #e74c3c
);

@each $name, $color in $theme-colors {
  .btn-#{$name} {
    background-color: $color;
  }
}
```

#### Resulting CSS

```css
.btn-primary {
  background-color: #3498db;
}

.btn-secondary {
  background-color: #2ecc71;
}

.btn-danger {
  background-color: #e74c3c;
}
```

### Nested Iteration

`@each` can be nested to iterate over multiple lists or maps simultaneously, providing powerful capabilities for generating complex styles.

#### Example with Nested Iteration

```scss
$sizes: small, medium, large;
$colors: red, green, blue;

@each $size in $sizes {
  @each $color in $colors {
    .box-#{$size}-#{$color} {
      font-size: if($size == small, 12px, if($size == medium, 16px, 20px));
      background-color: $color;
    }
  }
}
```

#### Resulting CSS

```css
.box-small-red {
  font-size: 12px;
  background-color: red;
}

.box-small-green {
  font-size: 12px;
  background-color: green;
}

.box-small-blue {
  font-size: 12px;
  background-color: blue;
}

.box-medium-red {
  font-size: 16px;
  background-color: red;
}

.box-medium-green {
  font-size: 16px;
  background-color: green;
}

.box-medium-blue {
  font-size: 16px;
  background-color: blue;
}

.box-large-red {
  font-size: 20px;
  background-color: red;
}

.box-large-green {
  font-size: 20px;
  background-color: green;
}

.box-large-blue {
  font-size: 20px;
  background-color: blue;
}
```

### Using `@each` with Complex Structures

You can also use `@each` to iterate over more complex data structures, such as lists of maps.

#### Example with List of Maps

```scss
$buttons: (
  (name: primary, color: #3498db, border: 1px solid #2980b9),
  (name: secondary, color: #2ecc71, border: 1px solid #27ae60),
  (name: danger, color: #e74c3c, border: 1px solid #c0392b)
);

@each $button in $buttons {
  .btn-#{map-get($button, name)} {
    background-color: map-get($button, color);
    border: map-get($button, border);
  }
}
```

#### Resulting CSS

```css
.btn-primary {
  background-color: #3498db;
  border: 1px solid #2980b9;
}

.btn-secondary {
  background-color: #2ecc71;
  border: 1px solid #27ae60;
}

.btn-danger {
  background-color: #e74c3c;
  border: 1px solid #c0392b;
}
```

### Summary

The `@each` directive in SCSS is an essential tool for iterating over lists and maps to generate dynamic, repetitive styles efficiently. It allows for cleaner, more maintainable code by avoiding redundancy and adhering to the DRY principle. By leveraging `@each`, you can create flexible and scalable stylesheets that can adapt to changing requirements with minimal effort.


### Detail explanation map-get

In SCSS (Sassy CSS), `map-get` is a built-in function used to retrieve the value associated with a specific key in a map. Maps in SCSS are collections of key-value pairs, and `map-get` allows you to access the value for a given key efficiently.

### Syntax

```scss
map-get($map, $key)
```

- `$map`: The map from which you want to retrieve the value.
- `$key`: The key whose corresponding value you want to retrieve.

### Example of Using `map-get`

Let's explore how `map-get` works with some examples.

#### Example 1: Basic Usage

```scss
$colors: (
  primary: #3498db,
  secondary: #2ecc71,
  danger: #e74c3c
);

.primary-color {
  color: map-get($colors, primary);
}

.secondary-color {
  color: map-get($colors, secondary);
}

.danger-color {
  color: map-get($colors, danger);
}
```

#### Resulting CSS

```css
.primary-color {
  color: #3498db;
}

.secondary-color {
  color: #2ecc71;
}

.danger-color {
  color: #e74c3c;
}
```

#### Example 2: Nested Maps

You can also use `map-get` with nested maps.

```scss
$themes: (
  light: (
    background: #ffffff,
    text: #000000
  ),
  dark: (
    background: #000000,
    text: #ffffff
  )
);

.light-theme {
  background-color: map-get(map-get($themes, light), background);
  color: map-get(map-get($themes, light), text);
}

.dark-theme {
  background-color: map-get(map-get($themes, dark), background);
  color: map-get(map-get($themes, dark), text);
}
```

#### Resulting CSS

```css
.light-theme {
  background-color: #ffffff;
  color: #000000;
}

.dark-theme {
  background-color: #000000;
  color: #ffffff;
}
```

### Practical Use Case: Combining with `@each`

`map-get` is often used in conjunction with the `@each` directive to dynamically generate styles based on map values.

#### Example 3: Generating Button Styles

```scss
$buttons: (
  primary: (
    background: #3498db,
    border: 1px solid #2980b9
  ),
  secondary: (
    background: #2ecc71,
    border: 1px solid #27ae60
  ),
  danger: (
    background: #e74c3c,
    border: 1px solid #c0392b
  )
);

@each $name, $styles in $buttons {
  .btn-#{$name} {
    background-color: map-get($styles, background);
    border: map-get($styles, border);
  }
}
```

#### Resulting CSS

```css
.btn-primary {
  background-color: #3498db;
  border: 1px solid #2980b9;
}

.btn-secondary {
  background-color: #2ecc71;
  border: 1px solid #27ae60;
}

.btn-danger {
  background-color: #e74c3c;
  border: 1px solid #c0392b;
}
```

### Some built-in functions

SCSS (Sassy CSS) offers a variety of built-in functions that help streamline the process of writing and managing stylesheets. These functions can be categorized into several groups based on their purposes, such as color functions, list functions, map functions, number functions, string functions, selector functions, and introspection functions.

### Color Functions

SCSS provides a comprehensive set of functions to manipulate and work with colors:

- `rgb($red, $green, $blue)`: Creates a color from red, green, and blue values.
- `rgba($red, $green, $blue, $alpha)`: Creates a color from red, green, blue, and alpha (transparency) values.
- `red($color)`: Gets the red component of a color.
- `green($color)`: Gets the green component of a color.
- `blue($color)`: Gets the blue component of a color.
- `mix($color1, $color2, [$weight])`: Mixes two colors together.
- `lighten($color, $amount)`: Makes a color lighter.
- `darken($color, $amount)`: Makes a color darker.
- `saturate($color, $amount)`: Increases the saturation of a color.
- `desaturate($color, $amount)`: Decreases the saturation of a color.
- `adjust-hue($color, $degrees)`: Changes the hue of a color.
- `complement($color)`: Returns the complementary color.
- `invert($color)`: Inverts a color.
- `grayscale($color)`: Converts a color to grayscale.

### Number Functions

These functions perform operations on numbers:

- `abs($number)`: Returns the absolute value of a number.
- `ceil($number)`: Rounds a number up to the nearest whole number.
- `floor($number)`: Rounds a number down to the nearest whole number.
- `round($number)`: Rounds a number to the nearest whole number.
- `percentage($number)`: Converts a number to a percentage.
- `unit($number)`: Returns the unit of a number.
- `unitless($number)`: Checks if a number has no unit.
- `min($numbers...)`: Returns the smallest number from a list of numbers.
- `max($numbers...)`: Returns the largest number from a list of numbers.

### String Functions

String functions allow you to manipulate strings:

- `quote($string)`: Adds quotes to a string.
- `unquote($string)`: Removes quotes from a string.
- `str-length($string)`: Returns the length of a string.
- `str-insert($string, $insert, $index)`: Inserts a substring into a string.
- `str-index($string, $substring)`: Returns the index of the first occurrence of a substring.
- `str-slice($string, $start-at, [$end-at])`: Extracts a substring from a string.
- `to-upper-case($string)`: Converts a string to uppercase.
- `to-lower-case($string)`: Converts a string to lowercase.

### List Functions

List functions help with list operations:

- `length($list)`: Returns the length of a list.
- `nth($list, $n)`: Returns the nth item in a list.
- `set-nth($list, $n, $value)`: Replaces the nth item in a list.
- `join($list1, $list2, [$separator])`: Joins two lists into one.
- `append($list, $value, [$separator])`: Appends a value to a list.
- `zip($lists...)`: Merges multiple lists into a single list of lists.
- `index($list, $value)`: Returns the position of a value within a list.

### Map Functions

Map functions are used for working with maps (key-value pairs):

- `map-get($map, $key)`: Returns the value for a given key in a map.
- `map-merge($map1, $map2)`: Merges two maps into one.
- `map-remove($map, $keys...)`: Removes one or more key-value pairs from a map.
- `map-keys($map)`: Returns a list of all keys in a map.
- `map-values($map)`: Returns a list of all values in a map.
- `map-has-key($map, $key)`: Checks if a map contains a given key.

### Selector Functions

Selector functions provide tools for working with CSS selectors:

- `selector-nest($selectors...)`: Nests one or more selectors within another.
- `selector-append($selectors...)`: Appends one or more selectors to another.
- `selector-extend($selector, $extendee, $extender)`: Extends a selector.
- `selector-replace($selector, $original, $replacement)`: Replaces a part of a selector with another.
- `selector-unify($selector1, $selector2)`: Unifies two selectors into one.
- `is-superselector($super, $sub)`: Checks if one selector matches all elements matched by another.
- `simple-selectors($selector)`: Splits a compound selector into a list of simple selectors.

### Introspection Functions

Introspection functions allow you to inspect and analyze values:

- `type-of($value)`: Returns the type of a value (`string`, `number`, `color`, `list`, `map`, `function`).
- `unit($number)`: Returns the unit of a number.
- `unitless($number)`: Checks if a number is unitless.
- `inspect($value)`: Returns the string representation of a value.
- `variable-exists($name)`: Checks if a variable exists.
- `global-variable-exists($name)`: Checks if a global variable exists.
- `function-exists($name)`: Checks if a function exists.
- `mixin-exists($name)`: Checks if a mixin exists.

### Miscellaneous Functions

There are also some miscellaneous functions for special purposes:

- `if($condition, $if-true, $if-false)`: Returns one of two values based on a condition.
- `unique-id()`: Generates a unique ID.

### Example Usage

Here's a practical example demonstrating a few of these functions:

```scss
$base-color: #3498db;
$colors: (
  primary: $base-color,
  secondary: lighten($base-color, 20%),
  danger: darken($base-color, 20%)
);

@each $name, $color in $colors {
  .btn-#{$name} {
    background-color: $color;
    color: if($name == danger, white, black);
    border: 1px solid adjust-hue($color, 10deg);
  }
}
```

#### Resulting CSS

```css
.btn-primary {
  background-color: #3498db;
  color: black;
  border: 1px solid #3aa6d4;
}

.btn-secondary {
  background-color: #5dade2;
  color: black;
  border: 1px solid #66b3e7;
}

.btn-danger {
  background-color: #2874a6;
  color: white;
  border: 1px solid #307db2;
}
```

In this example:
- `lighten`, `darken`, and `adjust-hue` manipulate colors.
- `if` applies conditional logic.
- `map-get` retrieves values from a map.
- `@each` iterates over a map to generate styles dynamically.
