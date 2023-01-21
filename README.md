# SASS_Lectures
# In-depth learning about SASS

```
Variables
// Declaring SCSS global variables, no curly braces needed, prepend '$' in front of the variables when declaring
$background-color: #333;
$text-color: rgb(228, 220, 220);
$highlight-color-pink: #bf4080;
$highlight-color-pink-hover: #c0548a;
$highlight-color-blue: rgb(60, 159, 240);
$font-family: Arial, Helvetica, sans-serif;

Maps
// Defining Maps variable which has multiple values with normal braces as wrapper and end it with semi-colon, example below
$font-weights: (
"light": 400,
"medium": 600,
"bold": 700,
);

$text-aligns: (
"start": start,
"center": center,
"end": end,
);

$mobile-breakpoints: (
"mobile": 578px,
"tablet": 992px,
"desktop": 1920px,
);

Nesting
// Simple SCSS Nesting example
body {
 background: $background-color;
 color: $text-color;
 margin: 50px auto;
 display: inline-block;
 font-family: $font-family;

// Importing and assigning theme mixin here and assiging to the light class and passed the variables as params as boolean values
 &.light {
  @include theme($dark-theme: true);
 }
}

Partials
// Importing Partials into the main.scss file, notice that no undesrcore needed or url() method needed to import partials, can omit the _ and .scss extension
// Naming convention for partial files, example _variables.scss, partial files has appended underscore on their file name
// This is one way of splitting files across multiple related to different components and imported back into main file
@import './resets';
@import './variables';
@import './functions';
@import './mixin';

Functions
// Note: Functions are used to compute values or return values
// Functions in SCSS has similar syntax to Javascript functions, where it takes params or args and returns SCSS built in functions or new output based on existing variables

@function weight($weight-name) {
// for accessing Maps based variables declared atr main.scss, use map-get syntax where it takes 2 params, first is variable name and 2nd is key of the pairs declared
// within the Maps variable as below example, eg: map-get($font-weights, bold);
 @return map-get($font-weights , $weight-name);
};

@function text-alignment($align-name) {
 @return map-get($text-aligns, $align-name);
}

Mixins
/// Note: Mixins are used to define styles that are reusable
// Mixin allows to reuse the scss codes across different elements that has same values, this is DRY concept of SCSS, where you can nest multiple css codes that similar and
// name it appropriately in this case marginBottom fits the content of code nested inside the mixin, and can reused globally
@mixin marginBottom {
  margin-bottom: 1rem;
}

// similar to function, mixin also can take arguements or params, for example as below
@mixin flexCenter($direction) {
  display: flex;
  flex-direction: $direction;
}

// Dark or Light theme mixin, where a named param is passed and a boolean value is assigned while passing into it when creating the mixin
@mixin theme($dark-theme: true) {
  @if ($dark-theme == false) {
   // lighten and darken is a built in method by SCSS, where it takes 2 arguements, first is the variable needs change and 2nd is invert it to how many percentage
   background: lighten($background-color, 100%);
   color: darken($text-color, 100%);
   color: darken($highlight-color-pink, 100%);
   color: darken($highlight-color-pink-hover, 100%);
   color: darken($highlight-color-pink, 100%);
  }
}

// Mixin for dynamic media query or mobile responsiveness
@mixin mobileResponsive {
  @media (width <= map-get($mobile-breakpoints, tablet)) {
  // @content syntax is similar to Vue's slot where you can reuse this mixin and populate relevant styles based on the breakpoints stated
  @content;
 }
}

Extend
#{&}__paragraph1 {
 // We are reusing the weight() function declared in _functions.scss file and passing the param as declared in _variables.scss
 font-weight: weight(light);
 @include marginBottom;

 // adding mobileResponsive mixin for mobile view on the element
 @include mobileResponsive {
  text-align: text-alignment(start);
 }

 &:hover {
  color: $highlight-color-blue;
 }
}

// Extend is an extension if styles inherits from one element to another, as you see using @extend followed by the class name we gonna extend,
// for example as below, we are re-using main__paragraph1's styles to main__paragraph2 and so on, but we also can add more style into extended class where it takes priority
// over the inherited class
#{&}__paragraph2, #{&}__paragraph3 {
 @extend .main__paragraph1;

 // this hover class has different styling from inherited styling, and it takes priority over the inherited ones
 &:hover {
  color: $highlight-color-pink-hover;
 }
}

Math Operations
// in CSS we need calc() method, but in SCSS we dont need that method to perform Math operations
// Noted: In SCSS we can only perform math operation of the same type, like 80%- 50%, but we can't do 80% - 30px, we can override this using CSS's calc() method here
// which works fine on SCSS should that need arises
width: 100% - 10%;
```
_____________________________________________________________________________________________________________________________

# Visit SASS Docs [Demo](https://rubanero14.github.io/SASS_Lectures)
_____________________________________________________________________________________________________________________________

# Source: [fCC](https://www.youtube.com/watch?v=_a5j7KoflTs)


