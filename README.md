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
### Variables:
To create a variable in LESS we just need to add a @ sign and declare it:
eg. 
@main-color:Blue;

And to use it:
background: @main-color;

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
