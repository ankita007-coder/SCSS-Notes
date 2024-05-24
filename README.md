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
