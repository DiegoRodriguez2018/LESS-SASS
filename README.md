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





