java c
CS152 
Lab Exercise 8: Dictionaries and Class Inheritance
This project continues our work with classes within the domain   of   physical   simulations.   This   is the second   part of a   multi-part   project where we will look at   increasingly complex   physical   simulations. This week we incorporate class inheritance,   more custom   shapes,   and sophisticated collisions.
Lab Tasks (L1-L3) 
L0. Setup 
Make one folder called Project_08 where you   keep your CS   152 files. Then copy   the   Zelle graphics   package and your physics_objects.py   into this folder.   In the project we   are   going   to we   are going to use a dictionary as   a   “router”   or   “selector” for what   type   of collision   is   required.   Just   in case you are still a little   rusty   on   dictionaries we will   start   with   a   quick   review   and   an   exercise.
You can watch a video about dictionaries from   Prof.   Maxwell:Dictionaries 
L1. Review Exercise on Dictionaries 
Dictionaries are a different   method of storing   information. A dictionary   is a   data type   like   a   list,   but the   information   in a dictionary   is   not stored   in sequential order.   Instead, each   value   stored   in   a dictionary   has a   unique   key.   In a dictionary,   the   key   plays the same   role   as   the   index   in   a   list.         The difference   is that a   key can   be any   Python type that   is   immutable   (can't   be   modified).   These   include the types   int, str, float, and tuple.   Examples of valid keys   are:
1,   42,   '42   ',   'ice   cream   ',   'chocolate   ',   'cookie   ',   1.7, and   (5,
'blueberry   ',   'muffins   ').
Create a   new   Python file called wordmap.py.   Put your name and   a   date   at the   top   of the file   in      a file   header (triple quotes), then start a   main function   (no   parameters). The   goal   of this   program   is to give the   user a set of word   prompts and then   record their   answer.   To   record   the   answer, use a dictionary with the word as the key   and the   response   as   the   value.   The   pseudocode   to   do   this   is   below: 
1.       Print out a   prompt for the   user that tells   them what   to   do.
2.       Create a list of about ten words, call   it   words.   Leave   space   after   each word   (ex:   “yes_”, “no “   ,   …   )
3.       Create   an   empty   dictionary, called   mapping   ={}.
4.       Loop over the    words list.   Each time   through   the   loop,   do   two   things.   First,   assign   a   response the return value of input, using the   word   as   the   argument   to   input.   Second,   using the word as the key for the empty dictionary mapping,   assign   to your dictionary the response (the   output from   input).
5.       Finally,   loop over the   keys   in mapping   (for key   in   mapping.keys   ())   and   print   out the   key/response   pairs   using the dictionary       .get   (key)   method to show the user their results.
L2. Refactoring (rewriting) our Classes with Inheritance 
Watch a video from   Prof.   Maxwell about inheritance: Inheritance 
Inheritance is sharing the capabilities of one class with one or   more   other   classes.   This week   we are going to use inheritance to simplify   the   code   in   the   physics_objects.py   file   and make   it easier to create   new   kinds of shapes. The goal   is to   create   a parent class,   Thing,   that   has all of the common fields and methods for   physical   objects. Then we   will   create child classes, like Ball, Block, and      Triangle,   that   make   use   of the   parent   Thing   class.
a. Define a parent class named Thing 
Edit your physics_objects.py file so   that it now   has   a   Thing   class   defined   in   it.   Add a comment   indicating that this class is the   parent   class for   simulated   objects.
b. Define the Thing   init  method 
The   init   method for Thing   should have   two   required   parameters,   win   and   the_type. The win   parameter will be the GraphWin window for drawing and the_type   will be the type of thing   being created   (e.g.   a   string   like   'ball'   or   'block').
You can add any number of default   parameters for the   remaining fields   later   on.
In the   init   method, create   the following   fields   and   assign   them   either   a   reasonable default value or their corresponding parameter.
type                                                                      A string,   indicating   the   type   of the   object.      (e.g.,   self.type
=   the_type)
mass                                                                   A scalar value indicating the mass   of the object.
position                                                       A 2-element list indicating   the   current   position   of the   object.
velocity                                                       A 2-element   list   indicating the   current   velocity   of the   object.
acceleration                                  A 2-element list indicating acceleration   acting   on   the   object.
elasticity                                                   The amount of energy   retained after a   collision.
scale                                                             代 写Lab Exercise 8: Dictionaries and Class InheritancePython
代做程序编程语言      The scale factor between the simulation   space   and   pixels.
Default to   10.
win                                                                            A reference to the GraphWin   object   representing the window.
vis                                                                               An   empty list   that   will   hold   Zelle   graphics.
color                                                                      An (r, g,   b) tuple. A good default value   is   black   (0,   0,   0).
drawn                                                                A boolean   indicating   if the shape   has been drawn,   initially False.
c. Create the get methods 
Create get   methods for all of the above fields except vis, win, and   drawn.   For   most   of them,   you can copy and paste the   code from   the   classes from   last week.
d. Create draw and undraw methods 
The draw method should loop over the   self.vis   list   of graphics   objects   and   draw   them   into the window specified by   self.win. The draw   method should finish   by   setting self.drawn   to True.
The und   raw   method should also loop over the   self.vis   list of graphics   objects   and   undraw each one. The undraw method   should finish   by   setting   self.drawn   to   False.
e. Create the set methods Create set methods for all of the above fields except   type, position,   scale,   win, vis, color, and drawn.   These   methods will   all   be   simple   and   should   only   update   the   value of the corresponding field.
f. Create the setPosition method 
def   setPosition   (self,   px,   py):
There   is   no change from last week's function.
1.       Calculate the difference   between the   new   position (px,   py) and the   current   position (i.e. self.position[0] and self.position[1]).   Put these values   in dx and   dy.
2.       Update the ball's   position fields with the   new   position.
3.       Multiply dx by   self.scale   and   dy   by   -self.scale.
4.       In a for loop,   move   all   of the   items   in the   vis   list   by   dx   and   dy.
g. Create the setColor method 
def   setColor   (self, c):   #   takes   in   an   (r,   g, b)   tuple
For the   setColor method first set the color field to       c. Then,   if c   is   not   None,   it   should         loop over the   self.vis   list and set the fill color of each object   to   the   specified   color.   You   may want to override this   method   in the child classes. (Remember   to   use gr.color_rgb   () to convert the three values   in c   into   a   Zelle   color   object.   e.g.   ((gr.color_rgb   (c   [0],c   [1],c   [2]))
h. Create an update method 
The update   method   is   identical to the   prior week's   method from the   Ball class.   It should update the simulated   position and velocity using the standard   equations   of   motion.   It   should   also move the graphics objects the   appropriate   amount. 
L3. Create a new Ball class that inherits from the Thing class 
class   Ball(Thing):
The   Ball class will need four methods,   init   ,   refresh, getRadius, and setRadius.
a. Define the   init  method 
The   init   method should   have win as the   only   required   argument,   but you   may
also want to add radius, x0, y0, and color   as   default   arguments   so   you   can   create   a   Ball   in a location (x0,   y0),   of a   particular   size   and   color.
The first step   in the    init   method   is to   call the   Thing   (parent)   init   method.   Call   it   by   using the   name of the class,   Thing, followed   by the   name of the   method,
init   , connected   by a dot (. The first three   arguments   should   be   self,   win,   and   the   string   "ball".
Thing.   init   (self, win,   "ball")
b.         You   may also want to   pass   in other parameters   if you   have them as optional   arguments      to the   Thing   init   method. Second, create a field   self.radius   and assign   it               the   radius   of the   Ball. Third, call   self.refresh   (), which   is a function that will define   the vis   list.
Finally, call   self.setColor   ().
c. Define a refresh method 
The refresh method should   implement the following   algorithm.
Assign to a local variable   (e.g. drawn)the   value   of   self.drawn
if   drawn:
undraw the object   (use   self.undraw   ())
Define the self.vis list of graphics   objects   using   the   current   position,
radius, and window
if   drawn:
draw the   object
To define the vis   list you can use   the   same   code   as   last   week.
d. Define getRadius and setRadius def   getRadius   (self):
The get   Radius   method should return the current value of the   radius field.   def   setRadius   (self, r):
The set   Radius   method should assign r to the   radius field   and then   call   self.refresh   ().
Once   you   have   completed   this, download   the   files   test_ballclass.py   and .py.   Put them   both   in the same folder as your new   physics_objects.py file.
Running   test_ballclass.py   should create two balls and send them   into a   single   collision.   When you are done with the lab   exercises,   begin the   project.



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
