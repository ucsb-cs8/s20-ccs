---
layout: lab
num: lab04
ready: true
desc: "input, scripts, command line arguments"
assigned: 2017-08-25 11:00:00.00-7
due: 2017-08-30 16:50:00.00-7
submit_cs_pnum: 776 
convert_lab: lab01
csxx: cs20
---



# What this lab is about

In this lab, we begin to move in the direction of writing real Python programs
that resemble the ones created by professional software developers to
solve real world problems.

Our first programs will still be very simple, and will not necessarily
<em>seem</em> very authentic.  They will do very simple tasks that, quite
honestly, can be done more easily with a simple calculator, for example.

I'll ask you to trust me that we are taking small steps that will get
larger as we move forward.

More specifically, in this lab, we want to learn four things:


1. Reusing a file we've already created by importing it as a module.
2. Writing an interactive program using `input` and `print`
3. Using the `if __name__=="__main__":` idiom so our programs can serve
   more than one purpose.
4. Using command line arguments (e.g. `sys.argv`)

Here's a bit more detail about each of these:

1.  Reusing a file we've already created by importing it as a module.

   Up until now, when we typed `import` we were always importing something
   that was part of the Python standard library, for example:

   ```
   import math
   import pytest
   ```
   etc.

   However, it is not only possibly, but <em>very</em> common, for
   programmers to <em>create their own modules</em> and import them.

   In fact, in this lab, we are going to take the functions you wrote
   for [{{ page.convert_lab }}](/lab/{{ page.convert_lab }}) in the file `convert.py` and import those
   so that they can be reused in this lab.  Since those functions already
   have test cases, and those test cases are passing, we have confidence
   that we can build software on top of those functions.

2. Writing an interactive program using `input` and `print`.

   Up until now, we've provided input to our functions in one of two ways:

   *   Hard coded values.

       For example, in lab01, we used hard coded function calls such
       as `drawA(100,50)`.  We call the values `100` and `50` "hard
       coded", because they are the same every time we run the
       program.

   *   Typing function calls directly at the Python Prompt (`>>>`).

       For example, in {{ page.convert_lab }}, we typed things like `fToC(32)` at the
       `>>>` prompt and looked to see what was returned by the
       function.  We could change the value passed to the `fToC`
       function by putting different argument values inside the
       parentheses.

   Most real world users of software don't work with a system such
   as the Python prompt.  In real software input values are usually provided
   through a mobile app, a web form, a graphical user interface (GUI).

   In old-school console apps, though, which is what intro students usually
   learn first, there are two ways of providing input.

   The first of these is using something like the `input` function
   which was covered in Chapter 3 of the textbook.  We also asked you about it
   on [Homework Assignment h04](/hwk/h04/)&mdash;in this lab, we'll put that
   knowledge to work.

   I mentioned on [Homework Assignment h04](/hwk/h04/), that while the author
   suggest the use of the `eval` function for getting non-string input
   from the user, I <em>strongly recommend</em> against getting into this
   habit.   We'll explore better ways of doing that in this lab.

   (Using any kind of `eval` function on user input, whether in Python
   or any other language, is a very risky practice, and a classic
   vector for malware to infect your system.  And, its not even the
   best approach.  Just say no to `eval` unless you REALLY know what you
   are doing.)

3. The use of command line arguments via `sys.argv`

   I said above that there two "old school console app" ways of getting
   input.  The way that most Unix commands get their input is through
   command line arguments.  You may not have thought much about it, but
   every time you use a command such as any of these, you are running
   a program:

   * <tt>cd {{ page.csxx }}</tt>
   * <tt>mkdir {{page.num}}</tt>
   * <tt>python3 -m pytest lab03.py</tt>

   The first thing on the line, e.g. `cd`, `mkdir`, or `python3`, is the name
   of the program you are running.  The rest of it is provided as input
   to the program.   We'll learn how you can do the same thing in your own
   Python code.
   

4. The use of the `if __name__=="__main__":` idiom in Python.

   This is an issue that can be a little confusing for students, but
   it really is quite simple.  This little strange looking piece of code
   allows us to use any Python file for two different purposes:

   * It does one thing when we <strong>run</strong> it
   * It can do something else entirely, when we <strong><tt>import</tt></strong>

  It's a very simple, yet  powerful feature, and we'll explore why its a
  really good habit to develop in your Python coding.


5. The use of the shebang to run Python programs as standalone programs.

   In the real world, when folks run a program, they run it to get something
   done.

   For example, earlier this week, I wrote a script that takes a class roster and
   creates a randomized seating chart for giving an exam in Phelps 1924.

   Suppose another faculty member is teaching in Phelps 1924 and wants to use
   my script.  What they care about is running the program and getting the
   result.  They really don't care whether its written in Python, or FORTRAN,
   or Java.   They just want to run it and get the output.

   On Unix/Linux and on MacOS, there is a easy technique called the "shebang" that we can use to turn
   any Python file into a "standalone program" that can be run at the
   terminal prompt.

   (Note: This shebang thing isn't applicable to old school Windows systems,
   though Windows 10 users probably can do it if they install either 

   * the "git bash shell" which is part of [Git for Windows](https://git-scm.com/download/win) or 
   * the new  [Windows 10's bash shell](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/).  
   
   Getting those to work is left
   as an exercise to the student though.  In any case, for Windows users,
   I <em>strongly encourage you to do
   this particular lab on CSIL</em>, through MobaXTerm if needed, and then try it out on your own system later.

Ok, we are ready to get started.




# Step 1: Make a <tt>~/{{page.csxx}}/{{page.num}}</tt> folder

The easiest way to create this is to do the following, which
will work from any directory:

<tt>mkdir -p ~/{{page.csxx}}/{{page.num}}</tt>

That form of the `mkdir` command, with the `-p` has these advantages:

*  It creates the entire path of directories in case any of the intermediate
   ones don't exist (that is, it will create a <tt>~/{{page.csxx}}</tt> directory too if it
   isn't there yet).

*  If the directory being create already exists, it won't complain

*  Since the directory being created starts with `~`, it's an absolute
   path.  That is, it is a specfic path all the way from the
   root directory (`/`), through any intermediate directories
   all the way down to the <tt>{{ page.num }}</tt> directory
     
   Because it is an absolute path, this command <em>does the right thing,
   regardless of what your current working directory happens to be.</em>

   That is an important point, and worth making sure you understand before
   your next exam. (That's a hint.)

Ok, once you've created this directory, to get yourself into it, type:

<tt>cd ~/{{page.csxx}}/{{page.num}}</tt>

Again, since that's an absolute path, it works from any directory.

# Step 2: Create a file called <tt>{{page.num}}</tt> in your <tt>~/{{page.csxx}}/{{page.num}}</tt> directory

To start out {{page.num}}, write the line:

```
import convert
```

That line is going to import the convert.py file that we wrote in {{ page.convert_lab }}.

Of course, that will only work if the convert.py file is in our current
working directory. So, next, we'll get that file where it should be.

First, though, use the "Save" command to save your {{page.num}}.py file.

# Step 3: Copy 'convert.py' from your <tt>{{ page.convert_lab }}</tt> directory to your <tt>{{ page.num }}</tt> directory

I realize that you may be working on the same computer, or a different one from the one where you did {{ page.convert_lab }}.  And, it's also possible that you didn't put your `convert.py` file in the "right place", i.e. in your <tt>~/{{page.csxx}}/{{ page.convert_lab }}</tt> folder.

No worries.  We are going to proceed as follows:

* First, we'll make sure you *have* a <tt>~/{{page.csxx}}/{{ page.convert_lab }}</tt> on the computer where you are working.
* Next, we'll make sure that that directory contains a good copy of your `convert.py` file from {{ page.convert_lab }}
* Finally, we'll go back to our <tt>~/{{page.csxx}}/{{page.num}}</tt> directory, and use a Unix command to copy the `convert.py` file over to that directory.

(NOTE: It may be tempting to just click and drag the file, using your
mouse to do the copying, and skip all command line stuff.  I
don't recommend that, because he process of copying files from
one Unix/Linux directory to another is likely to be on the next
exam in this course.  So it might be a good idea to actually
practice these steps.  Entirely up to you.)

Alright, let's dive in.  First, try this:


<tt>cd ~/{{page.csxx}}/{{ page.convert_lab }}</tt>


If it didn't work, because that directory doesn't exist on this computer,
or in this account, then create it like this, and try the cd command again:


<tt>mkdir -p ~/{{page.csxx}}/{{ page.convert_lab }}</tt><br>
<tt>cd ~/{{page.csxx}}/{{ page.convert_lab }}</tt></br>


(For an explanation of the `-p` flag, see the discussion earlier in this lab.)

Then, use the `ls` command to see if the file `convert.py` is in that directory:

```
ls
```

If the file is NOT THERE, then:

* Use your web browser to login to Gradescope
* Navigate to the page for {{ page.convert_lab }}
* Find your last submission
* Download the file and save it into your directory.

<div style="width:80%; margin-left:auto; margin-right:auto; background-color: #efe; border: 5px inset #3f3;" markdown="1">

## It's not working&mdash;what do I do?

A situation in which this will NOT work is if you are logged into CSIL via MobaXTerm, or `ssh -X` on MacOS.  

In this case, your web browser downloads the file to your computer's
hard drive, not to your CSIL directory.

There are two work arounds:

(1) Just copy paste the contents from the web page into a new file.

(2) Bring up a web browser running on CSIL by typing either `firefox` or `google-chrome` in at the CSIL prompt. Note: This method is not fun.   It typically runs very slowly, and you may see lots of error messages on the screen, and it will take a long time.  But eventually the Chrome or Firefox browser should appear.  It will hopefully work well enough for you to log into Gradescope and download your convert.py file into your <tt>~/{{page.csxx}}/{{ page.convert_lab }}</tt> directory.

</div>

Ok, assuming the `convert.py file is there, you can use one of these two commands to look at its contents.  We want to make sure that is looks like the "finished product" from your 

* `cat convert.py`
* `more convert.py`

Try both of those now.  You should see that `convert.py` file is your finished
product from {{ page.convert_lab }}.

Note that the `cat convert.py` file lists the entire contents of the file.  The thing is, if the file is long, it just spews out the entire thing all at once. 

The command `more convert.py` file *also* lists the contents of the file, but if the file is longer than a single screen of text, it gives it to us one screen full at a time, with the word `More` at the bottom of the screen.  We can press either Enter, or the space bar, to go through the file one line or one screen full at a time.  Try it a few times.

(There are other keys you can press as well, including `q` to quit in the middle of the file, as well as keys to search for particular text, and many other fun goodies.  To learn more about more, see [this tutorial](https://shapeshed.com/unix-more/) and this [wikipedia article](https://en.wikipedia.org/wiki/More_(command))).

Assuming that file is where it should be, i.e. in
the directory <tt>~/{{page.csxx}}/{{ page.convert_lab }}</tt>, we can now go back to your <tt>~/{{page.csxx}}/{{page.num}}</tt> directory with a cd command:


<tt>cd ~/{{page.csxx}}/{{page.num}}</tt>


Now, copy the `convert.py` file into your current directory with this command. This is the unix `cp` command which stands for "copy":

<tt>cp ~/{{page.csxx}}/{{ page.convert_lab }}/convert.py ~/{{page.csxx}}/{{page.num}}</tt>

After running this command, use `ls` to see if the `convert.py` file is there:

```
ls
```

If so, you are almost ready for the next step.

Before you go on though, a reminder that you can make a preliminary submission to Gradescope anytime you are "done for the day" (i.e. if you aren't completely finished with the lab, and are planning to come back to it later.)

The benefit is that this provides a way to move your files between CSIL and your own computer, and/or to share files between pair partners.

It's also a way you can put code in a place where the instructors can
see it in case you want to ask a question on Piazza via private
instructor note.  Upload your code first, then ask the question, and
note that you have a submission on Gradescope.  While you can only see
your own submissions on Gradescope (and those of your pair partner,
not no one else's), instructors have access to see all submissions for
the class.

Try making a submission to Gradescope now, and see whether you get any partial credit for the work done so far.

# Step 4: Go back to your <tt>{{page.num}}</tt> and run it

If you've followed the instructions up to this point,
your <tt>{{page.num}}</tt> file
(which should be located in your <tt>~/{{page.csxx}}/{{page.num}}</tt> folder) only has these contents:

```
import convert
```

That should be enough that we can run the file and see one of two things:

What we want to see:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
>>>
```

If that's what you see, good!  Move on to step 5.

What we don't want to see:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================

Traceback (most recent call last):
  File "/Users/pconrad/cs8/lab04/lab04.py", line 1, in <module>
    import convert
ImportError: No module named convert
>>> 
```

If you see the second thing (the error message), it suggests that you ran `idle3` from some directory other than your <tt>~/{{page.csxx}}/{{page.num}}</tt> directory where your `convert.py` program is located.

If you see the error, do this to get back on track (otherwise, just go on to th next step):

* Quit `idle3`
* make sure that your <tt>{{page.num}}</tt> and your `convert.py` are both in your <tt>~/{{page.csxx}}/{{page.num}}</tt> folder
* make sure that <tt>~/{{page.csxx}}/{{page.num}}</tt> is your current working directory (use `pwd` to check that)
* Start `idle3` again.


# Step 5: Learning about the `__name__=="__main__"` block

Ok, now we are ready to put some code in our {{page.num}}.py.

This is an important step to work through slowly and carefully, to get
the learning&mdash;not just to get the result.    There isn't much code
to write here, but there is a lot of important reading, and if you gloss over
it, you'll have trouble later.

The first thing we are going to put in there is this funny looking code right
here.  Just copy this in there for now, and I'll explain it in a moment.

(I've repeated the `import convert` that was already there, just for context.)

```
import convert

print("This is outside the main block of lab04.py")

if __name__=="__main__":
   print("This is the main block of lab04.py")


```

Note: make sure you type that line with the `if`  <em>exactly</em> as shown:
* The variable `__name__` must be exactly two underscore characters, followed by exactly this: `name`, followed by exactly two underscore characters. 
* The string `"__main__"` must be exactly two underscore characters, followed by exactly this: `main`, followed by exactly two underscore characters.
* It must be exactly two equals signs: `==`
* The only part that can vary is whether you use single or double quotes. `'__main__'` or `"__main__"` are both ok.

# What the heck does `__name__=="__main__"` mean?

The if test is checking whether a funny looking variable, `__name__` is equal to some other funny looking string `"__main__"`.  But why?

Basically, this funny variable equals this funny string whenever you run a Python program <em>directly</em>, as opposed to <em>importing it</em>.

We can see the effect by doing the following.  Let's load up your `convert.py` file in idle, and put this code at the very bottom of the file:

```
print("This is outside the main block of convert.py")

if __name__=="__main__":
   print("This is main block of convert.py")
```

Then, try choosing the "Run Module" command from the menu in idle, from the window where your file `convert.py` is open. You should see this:

```
>>> 
================ RESTART: /Users/pconrad/cs8/lab04/convert.py ================
This is outside the main block of convert.py
This is main block of convert.py
>>>
```

Then, run your <tt>{{page.num}}</tt> file using "Run Module".  You should see this:

```
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is outside the main block of convert.py
This is outside the main block of lab04.py
This is the main block of lab04.py
>>> 

```

Ok, what just happened?  Here's what:

* When you ran `convert.py` you saw the output of both lines of code: the one that was outside the `__name__=="__main__"` block, and the one inside the block.  That's because when you run the file directly, you see both.

* When you ran <tt>{{page.num}}</tt>, you saw the output of both lines of code in <tt>{{page.num}}</tt>, but you <em>also saw the line from outside the `__name__=="__main__"` block in `convert.py`</em>.

* You saw some output from `convert.py` when you ran <tt>{{page.num}}</tt> because you did `import convert`.

* But you ONLY saw the output from code that was OUTSIDE the `__name__=="__main__"` block.

* Code that is INSIDE a `__name__=="__main__"` block does NOT GET RUN when a file is imported.

* All other code IS executed both when a file is run, and when a file is imported.

With this as background, we can now clearly state the purpose of a `__name__=="__main__"` block:

<div style="width:80%; margin-left:auto; margin-right:auto; background-color: #efe; border: 5px inset #3f3;" markdown="1">

# What is a `__name__=="__main__"` block for?

It is good practice in Python to put ALL code other than function definitions
and initial assignments of global variables into a `__name__=="__main__"`
block.

That is, the main code for a Python program that does the work should ideally
always be in a  `__name__=="__main__"` block.

That allows us to <em>reuse</em> all of the other function definitions in our program
by <em>`import`ing them into another program</em> without any unwanted
side effects.

</div>

# Step 6: Remove the print statements outside the main block

So, our next step will be to remove the print statements in `convert.py`
and <tt>{{page.num}}</tt> that are outside the `__name__=="__main__"` block.  (We only put those in temporarily in this step so that you could understand how the
`__name__=="__main__"` block works.)

Specifically,
remove these lines:

From {{page.num}}.py, delete this line:


<tt>print("This is outside the main block of {{page.num}}.py")</tt>

From convert.py, delete this line:

```
print("This is outside the main block of convert.py")
```

Run your two files again, and see if your results match those shown below.

Note that when switching between two file windows in `idle3` you must actully click <em>inside</em> the window in `idle3` before you run&mdash;just bringing the window to the front isn't enough (you might still running `convert.py` when you think you are runnnig <tt>{{page.num}}</tt>, or vice-versa.)

For `convert.py`:

```
================ RESTART: /Users/pconrad/cs8/lab04/convert.py ================
This is main block of convert.py
>>> 
```

For <tt>{{page.num}}</tt>:

```
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
>>> 
```

If so, you are ready for the next step.

# Step 7: Using the `input` function 

Now, we'll show how your program can have a conversation with the
user.

Enter this into the main block of your <tt>{{page.num}}</tt> file, as shown below:

```

if __name__=="__main__":
   print("This is the main block of lab04.py")

   fTempStr = input("Please enter a Fahrenheit temperature: ")
   print("You entered: ",fTempStr)

```

Run the program.  You should see something like this:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
Please enter a Fahrenheit temperature:
```

Enter a temperature, e.g. `45` and press enter.  It should then look like this:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
Please enter a Fahrenheit temperature: 45
You entered:  45
>>>
```

Try this again, but this time enter something else.  You should see that whatever you type in gets echoed back.

When that's working, we'll try the next step, which is to convert the user input into a number.

# Step 8: Converting `input` data to a number

As you know from the reading in Chapter 3, and [Homework H04](/hwk/h04/), the `input` function returns string data (Python type `str`).  If we want to use this as a number, we need to do a conversion.  The textbook suggest using `eval`. DON'T DO THAT.  Here's what do to instead:

```
if __name__=="__main__":
   print("This is the main block of lab04.py")

   fTempStr = input("Please enter a Fahrenheit temperature: ")
   print("You entered: ",fTempStr)

   fTemp = float(fTempStr)
   cTemp = convert.fToC(fTemp)

   print("{} degrees F = {} degrees C".format(fTemp,cTemp))

```

Try this code, and try entering a few values for the Fahrenheit temperature.

First try some legit numbers.  For example:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
Please enter a Fahrenheit temperature: 68
You entered:  68
68.0 degrees F = 20.0 degrees C
>>>
```

Well, that's nice!  But what if we put in something invalid, for example "potato":

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
Please enter a Fahrenheit temperature: potato
You entered:  potato
Traceback (most recent call last):
  File "/Users/pconrad/cs8/lab04/lab04.py", line 10, in <module>
    fTemp = float(fTempStr)
ValueError: could not convert string to float: 'potato'
>>>
```

Well, that's unfortunate.  But, no worries: we can take care of it.

We'll do that in the next step.

# Step 9: Gracefully handling errors

Change these three lines of code:

```
   fTemp = float(fTempStr)
   cTemp = convert.fToC(fTemp)

   print("{} degrees F = {} degrees C".format(fTemp,cTemp))

```

Into these line of code:

```

   try:
      fTemp = float(fTempStr)
      cTemp = convert.fToC(fTemp)
      print("{} degrees F = {} degrees C".format(fTemp,cTemp))
   except ValueError:
      print("Sorry, I could not convert {} to a number".format(fTempStr))

```

Now, try again with both the valid and invalid input.  For valid input
such as 68 there should be no difference.  But for invalid, input
we should now see something like this:

```
>>> 
================= RESTART: /Users/pconrad/cs8/lab04/lab04.py =================
This is the main block of lab04.py
Please enter a Fahrenheit temperature: potato
You entered:  potato
Sorry, I could not convert potato to a number
>>> 
```

Ok, this is great!  But we can still do more!

# Step 9: Adding a shebang

Ok, now we are going to add another strange bit of code to our file.

The following line must be the VERY first line of the file, before
any imports, any other comments, any blank lines, and it must be truly
EXACTLY as shown.  Put this at the very top of your <tt>{{page.num}}</tt> file.

```
#!/usr/bin/env python3
```

Be sure to SAVE this change after making it in the `idle3` file window.

This is a bit of magic sauce that allows us to run the program directly
from the shell.  It is called a "shebang", and you can read more about it
here, including why it's called a "shebang":

* <https://ucsb-cs8.github.io/topics/shebang/>

This ONLY works on Linux and MacOS, so if you are working
on Windows, you need to do this part on CSIL if you want to see it work.

Bring up a terminal window. If your terminal window is running idle3,
you can use the special trick of pressing CTRL-Z, then `bg` followed
by enter to get your cursor back.

Then use `pwd` to make sure you are in <tt>~/{{page.csxx}}/{{page.num}}</tt>.  If not, put yourself
there.  Make sure, also, that you can see the <tt>{{page.num}}</tt> file (use `ls` to
list the files.)

If you can, then use this Unix command.  This makes your <tt>{{page.num}}</tt> executable:

```
chmod u+x {{page.num}}.py
```

Finally, type this at the Unix prompt (make sure you saved the file in `idle3` first):

```
./{{page.num}}.py
```

You should see the following:


```
[your unix prompt here]$ ./lab04.py
This is the main block of lab04.py
Please enter a Fahrenheit temperature: 68
You entered:  68
68.0 degrees F = 20.0 degrees C
[your unix prompt here]$
```

Whoa!  You just ran a Python program that:

* you ran at the command line, as if it were a unix command
* that you wrote yourself (granted, with some guidance)
* that reused a imported module that you wrote last week
* that asked for input, and printed a result
* and that fact that it happens to be a Python program is completely obscured from the user running the program.

This is where it actually starts to look like "real programming".

But wait, it gets even better.   We still have one more trick.

# Step 10: Command line arguments with `sys.arg`

Wouldn't it be cool if instead of having to type `./{{page.num}}.py` on one line
and then typing in temperature after we are prompted, if we could just
type:

```
./{{page.num}}.py 68
```

And it would just print the result?

Well, we can.  Here's how:

First, add this import near the top of the file, right before or after
your `import convert` (but not the *very* top, because the shebang has to
be the first line in the file.)

```
import sys
```

Replace this line of code:

```
  fTempStr = input("Please enter a Fahrenheit temperature: ")
```

With this:

```
  if len(sys.argv) >= 2:
     fTempStr = sys.argv[1]
  else:
     fTempStr = input("Please enter a Fahrenheit temperature: ")
```

Save this change. Now try this at the linux shell prompt:

```
./{{page.num}}.py 68
```

Then try this at the linux shell prompt:

```
./{{page.num}}.py
```

What you should see is a result like that shown below:

```
[your unix prompt here] $ ./lab04.py 68
This is the main block of lab04.py
You entered:  68
68.0 degrees F = 20.0 degrees C
[your unix prompt here] $ ./lab04.py
This is the main block of lab04.py
Please enter a Fahrenheit temperature: 32
You entered:  32
32.0 degrees F = 0.0 degrees C
[your unix prompt here] $ 

```

If your output looks similar, you are almost done.  A bit of reading
in Step 11, then submit at Step 12.

# Step 11: Taking stock of what we've done.

Ok!  That's a lot of stuff.  

This lab was pretty "cookbook"&mdash;for the most part, you were led by the hand through it.

If you did it all correctly, you should be able to submit your convert.py and {{page.num}}.py files to Gradescope, and get a perfect score right away.

If you don't get a perfect score, it's likely either because:

* (a) there may have been still some unresolved problem from your {{ page.convert_lab }} submission, or
* (b) there might be some very small formatting error in one of the strings (e.g. you wrote <tt>"This is the main blerg of {{page.num}}.py"</tt> instead of <tt>"This is the main block of {{page.num}}.py"</tt>

But most likely, you'll get a perfect score on the first try.


Now: you will have a follow up lab where you'll be asked to do all of the same things you did in this lab, but <em>without</em> the detailed instructions.  You'll need to refer back to this lab and <em>understand</em> what you did.

So, please make sure that you read back through this, and if any part of it doesn't make sense to you, <em>ask questions.</em>


# Step 12: See perfect score on Gradescope; profit.

Navigate to {{page.num}} on Gradescope, and upload your `convert.py` and `lab04.py` files.

At this point, you should see that you have a perfect 100 points on Gradescope, and
you are finished with the lab!

If not, go back through each step of the lab carefully to see if you overlooked any part of the instructions before asking questions.  If you are still not sure, then either:

* visit the [Open Lab Hours](https://ucsb-cs8-s18.github.io/info/s18_open_lab_hours/)
* visit the [Instructor's Office Hours](https://ucsb-ccs-cs20-s18.github.io/info/office_hours/)
