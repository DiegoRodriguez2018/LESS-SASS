# LESS
To use less we need to rename our styles.css to styles.less. We also need to intall globally the less package in node, or add the link and script files in the html to run on the client side.

The instructions for both of these options can be found on:

http://lesscss.org/


---
### LESS on the client side:
To run in client side, the code will look something like this:

  <!-- importing less files: -->
  <link rel="StyleSheet/less" href="css/init.less" type="text/css">
  <link rel="StyleSheet/less" href="css/my.less" type="text/css">

  <!-- importing less script: -->
  <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.9.0/less.min.js"></script>


Note that we need to modify rel to SyleSheet/less, otherwise the script won't be able to find the less files. 


---
### LESS on the server side:
There is support for Node.js, ASP.NET, and Rails. For node we just install the package globally:
`npm install -g less`

After installing globally we have access to the lessc (less compile) command from any directory. 

To compile a less file into a css file we do:
lessc [option option=parameter ...] <source> [destination]

eg.
`lessc bootstrap.less bootstrap.css`

Some popular options are:
Silent, Version, Help, Makefile.
 

---
### Comments

LESS supports both css comments (/* h1, */) and javascript comments (//h1)


---
### Variables:
To create a variable in LESS we just need to add a @ sign and declare it:
eg. 
@main-color:Blue;

And to use it:
background: @main-color;

Important to note that variables in LESS are CONSTANTS. You can not change their value later. 

We can store in variables:
  * Colors 
  * Units (eg. 1rem)
  * Strings (eg. Helvetica)
  * Complex types (1px solid black)

---
### Operations
eg.
font-size : 4px + 4;
color: #FFF / 4

---
### Color functions:
There are inbuilt color functions in LESS: 
eg.
color : lighten (@color, 10%);
color : darken (@color, 10%);

Popular functions include:
* Saturate
* Desaturate
* fadein
* fadeout
* fade
* spin (across the color wheel)
* mix (two colors)
* hue 
* saturation
* lightness
* alpha
* hsl

IMPORTANT: note that to use this functions the colors need to be declared by their numeric value (eg. #008000) not the string value (eg. green)

### Math functions:
* round
* ceil
* floor
* percentage


---
##Mixins
Mixin offers support for repeatable sections of css code. Mixins are like functions. 
To declare a Mixin we need to start with a dot followed by the name and the arguments:

eg. 
.rounded-corners-all(@size: 5px){
  border-radius: @size;
  -moz-border-radius: @size;
  -webkit-border-radius: @size;
}

Note that if @size is not supplied the default value will be 5px.

### Mixins Overload
This is similar to other languages overload, we can have two Mixins with the same name but different number of attributes:

eg.
.color(@color){
  color: @color;
}

.color(@color, @factor){
  color: lighten(@color, @factor);
}

\#form
{
  .color(#888, 20%); //uses 2nd overload
}

By calling .color and passing to attributes, LESS knows that the second Mixin is the one we are trying to call. 

---
### Mixins Guards
Guards are an extra layer of logic we can add to our Mixins:

.color(@color) when (alpha(@color) >= 50%){
  color: Black;
}

.color(@color) when (alpha(@color) < 50%){
  color: transparent;
}

\#form
{
  .color(@main-color); //uses 1st overload
}

So if the colors alpha value is bigger than 50% it will run the first Mixin, otherwise it will run the second one. 


We can also use type guards:

.width(@width) when (isnumber(@size)){
  width: @size *2;
}

.width(@width) when (ispercentage(@size)){
  width: @size;
}

\#form
{
  .width(50%); //uses 2st overload
}


---
## Nested Rules

LESS allow us to  write nested rules, eg:

nav
{
  font-size: 14px;
  font-weight: bold;
  float: right;
  ul
  {
    list-style-type: none;
    li
    {
      float: left;
      margin: 2px;
      a
      {
        text-decoration: none;
        &:hover
        {
          text-decoration: underline;
        }
      }
    }
  }
}

---
### Combinators
LESS recognises combinators (&). In the previous example text-decoration value will be node for all the anchors inside li, but note that if the anchor is also being hovered the value will change to underline. Important to note that there is no spaces in &:hover.

---
### String interpolation
To do string interpolation we need to type @{}
eg.
@root = '/images/'

\#form{
  background: url ("@{root}background.jpg");
  //will produce url("/images/background.jpg");
}

---
### Using Javascript inside LESS
We can use vanilla javascript if we need to:
@root = '/images/'
@app-root = `"@{root}".toUpperCase()`;

Note that @{} isjust string inperpolation. Also note that to evaluate javascript we need to use backticks ``

---
### Namespacing and Scope

We can add Mixins to a LESS component and then just call them where we need them.
\#contact-module {
  .fonts(){
    font-family: "Open Sans", Verdana, Helvetica, sans-serif;
    font-size: @base-size;
  }
}

  
input[type=textbox], textarea
{
  
  `#contact-module > .fonts();`

  background: #ffffe0;
  width: 250px;
  display: block;
  border: 1px #000 solid;

  .rounded-corners-all(6px);

  padding: 2px;
}

Note that to call the Mixin we just need to do #contact-module > .fonts(); Important to notice that @base-size runs on the scope of input, textarea{}. If we declare a new @base-size with a different value inside those components that will overide the global one. 

---
---
# SASS
SASS is similar to LESS, it stands for Syntatically Awesome StyleSheets, its a Dynamic Style Sheet Language and compiles to CSS just like LESS. 

SASS also has two syntaxes.
1. SASS: the original syntax and is based on indention (like python). It does not feel like CSS and CSS files are not valid SASS files. 
2. SCSS: is a more common syntax, it feels like CSS and CSS files are valid SCSS files. 


---
### SASS on the server side:
There is support for Node.js, ASP.NET, and Rails. There are also many install options including downloading the package from github and adding it to your path, homebrew for Mac and even some GUI applications.

For node we just install the package globally:
`npm install -g sass`

After installing globally we have access to the `sass` command.

`sass input.scss output.css`

A handy flag is --watch, this will tell sass to watch for file changes and recompile if they occur. 

`sass --watch input.scss:output.css`


---
### Variables:
Similar to LESS, but instead of @ we use the dollar sign $:
$main-color:Blue;

And to use it:
background: $main-color;

---
### Operations
SASS allows us to perform inline operations:
eg.
font-size : 4px + 4;
color: #FFF / 4

---
### Color functions:
SASS also have some inbuilt color functions:
color : lighten ($color, 10%);
color : darken ($color, 10%);

Popular functions include:
* Saturate
* Desaturate
* fadein
* fadeout
* invert
* complement
  
### Other functions:
Strings:
* quote ($sometext)
* unquote ($sometext)

Math:
* round
* ceil
* floor
* percentage

If method:
* $value: if(true, $color1, $color2);

---
### String interpolation
In SASS to perform string interpolation we need to use #{$<variable-name>}
eg.
$root = '/images/'

\#form{
  background: url ("#{$root}background.jpg");
  //will produce url("/images/background.jpg");
}

Note that in SASS we can use string interpolation anywhere in the scss file. For example:

$class-name : 'my-form';

.#{$class-name}{
  color:blue;
}

This will produce:
.my-form{
  color:blue;
}

An useful application of this would be:

$baseClassName : 'col';

.#{$baseClassName}-1{
  color:blue;
}

.#{$baseClassName}-2{
  color:red;
}


This will produce

.col-1{
  color:blue;
}

.col-2{
  color:red;
}

---
### Rules
SASS rules are very similar to LESS:

nav
{
  font-size: 14px;
  font-weight: bold;
  float: right;
  ul
  {
    list-style-type: none;
    li
    {
      float: left;
      margin: 2px;
      a
      {
        text-decoration: none;
        &:hover
        {
          text-decoration: underline;
        }
      }
    }
  }
}

Note that combinators (&) are also supported.

SASS also allows us to use nested properties, eg:

.button{
  font: {
    family: Vernada, Helvetica, sans-serif;
    size: 14px;
  }
}

This will produce:

.button{
  font-family: Vernada, Helvetica, sans-serif;
  font-size: 14px;
}
