---
assigned: 2020-01-22 19:30
desc: Even more functions with test cases
due: 2020-01-29 19:30
layout: lab
num: lab03
ready: true
---

In this lab, you'll get more practice with

* Writing functions
* Testing function with pytest
* Submitting your functions and test cases to Gradescope for grading


# Step 1: Verify that pytest is working on the machine where you plan to work.

You may choose to work on your own machine, or on a CSIL machine.  Either
way, you will need `pytest` installed.  

As in lab02, we check whether pytest is installed by doing the `import pytest` command
at the Python shell prompt.  If it returns no error message, then `pytest`
is installed.  If you get an error, refer back to
[lab02](/lab/lab02/) for instructions on installing it.

```
[cgaucho@csil-12 ~]$ python3
Python 3.4.3 (default, Aug 9 2016, 15:36:17) [GCC 5.3.1 20160406 (Red Hat 5.3.1-6)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pytest
>>>
```

# Step 2: Make a `~/cs8/lab03` folder

The easiest way to create this is to do the following, which
will work from any directory:

`mkdir -p ~/cs8/lab03`

That form of the `mkdir` command, with the `-p` has the advantage that

* It creates the entire path of directories in case any of the intermediate
   ones don't exist (that is, it will create a `~/cs8` directory too if it
   isn't there yet)
* If the directory being create already exists, it won't complain
* Since the directory being created starts with `~`, it's an absolute
   path, and thus the command works regardless of the current directory.

Then, to get yourself into that directory, type:

`cd ~/cs8/lab03`

Again, since that's an absolute path, it works from any directory.

# Step 3: Create a file called `lab03.py` in your `~/cs8/lab03` directory

To start out lab03, write the line:

```
import pytest
```

Then, copy this function definition into your
lab03.py file.

```
def areaRect(length,width):
   """
   Compute area of rectangle
   """
   return -42.0 # stub  @@@ replace this stub with the correct code @@@

   
```

Then, copy these function definitions into your file.  These are a special kind of function called a <em>test case</em>.  These particular test cases are written in the style used by the <em>pytest</em> testing framework, and they follow these rules:

1. The name of each test cases function must start with `test_` or end with `_test`.
2. Each one ends (typically) with a line of code that starts with the keyword `assert`, followed by a boolean expression.
   * If the expression is `True`, the test case <em>passes</em>
   * If the expression if `False`, the test case <em>fails</em>
3. Each test case function must have a different name (hence: `test_areaRect_1`, `test_areaRect_2`, `test_areaRect_3`, etc.)  They don't have to be consecutive numbers&mdash;we could use `_a`, `_b`, `_c` or anything really, as long as they are all different.

```

def test_areaRect_1():
   assert areaRect(3,4)==12

def test_areaRect_2():
   assert areaRect(0.5,0.4)==pytest.approx(0.2)

```

Finally, run the code, and ensure that you don't have any syntax errors
in your Python code.


# Step 4: Add a third test case that you write yourself

The third test case should be one that you come up with yourself. The restrictions are that it must be:

* a function called `test_areaRect_3`
* it should have an `assert` statement
* the assert keyword should be followed by a call to `areaRect` with some other argument values, different from the ones in the first two test cases, followed by a test for equality operator `==`, and the value that you expect `areaRect` to return for those argument values

Please write this third test case and save your lab03.py file before proceeding to the next step.

# Step 5: Test your code by hand

Because I want to be sure that you continue to practice the skill,
test your code by hand first.

That is, select "Run Module" in IDLE, and then type in a few function calls
at the Python Shell Prompt.   Here are a few:

```
>>> areaRect(4,5)
-42.0
>>> areaRect(7,3)
-42.0
>>> 
```

Ok, so that's sort of pointless as long as we haven't fixed the function yet.  The point
is that
* you need to know how to check the value of a function call by typing it in.
* you need to see that right now, the function *always* returns -42.0, no matter what.

There is a reason for that.  We call this a "stub value".  It returns the wrong answer
*on purpose* so that we can check that all of the tests fail.   We want to see all of
the tests fail, THEN see all of the tests pass.  That's the general idea.

* We want so see them *all fail* when the function is wrong
* Then if they *pass* when the function is right, we *trust* the test.

# Step 6: Run pytest on the file so far

As a reminder, you run pytest OUTSIDE of idle, at the regular terminal
prompt.

You may find it helpful to bring up a second terminal window and use

```
cd ~/cs8/lab03
```

to get into the correct directory.  Then use:

```
python3 -m pytest lab03.py
```

You should see three test failures. If you do, then you ready to fix the code so that it works, which is the next step.

(If you need a refresher on how to interpret
the output of `pytest`, refer back to [lab02](/lab/lab02/])


# Step 7: Fixing the code for `areaRect`

So, if you have failing test cases, the thing to do is fix the code so
that the test cases pass.

Once you have the code correct, try testing both using interactive testing as well as by running `pytest`.

# Step 8: Submit your partially completed work to Gradescope

You are by no means finished with this lab.   But, we want to encourage you to make
a submission to Gradescope now anyway.  Here is why:

1.  It provides a backup copy of your work in case something goes wrong with your
    computer or your CSIL account.
    
2.  It provides a staging ground for you to move your file between your laptop and CSIL.

3.  You also will be able to see some progress towards completion of the lab&mdash;
    partial credit for completion of this step.
    
Login to [gradescope.com](http://gradescope.com), navigate to this course, and look for {{page.num}}.

Navigate to that page, and upload your `lab03.py` file.

If you have done the steps so far, though most of the tests will fail, you 
should be able to earn at least some partial credit for having uploaded a file called <tt>{{page.num}}</tt>


# Step 9: Read these instructions about how the rest of the lab will work

In each of the steps that remain, you will add an additional function definition,
and some test cases.

You should try to make the function pass the test cases that you put in.

In some cases you'll be given the test cases.  In other cases, you have to supply
these test cases yourself.

At each step, you should first try to get the test cases to pass by running
pytest at the Unix command line as shown.

* Please do this BEFORE submitting to Gradescope
* Please DO NOT submit to Gradescope without testing locally first

Once you see that they are passing, THEN submit a version to Gradescope to see
if you also pass the instructor test cases for that step.

If you do, proceed to the next function definition and set of test cases.

If you pass your own tests, but NOT the instructor supplied tests, then try to
see if you can figure out why.  Is there some case that you did not consider?
The problems may have hints.

You can also ask questions on Piazza. This is a good situation to use a "private
post" to the instructors.  We can see your submissions on Gradescope
so you don't have to share your code with us--just tell us your name, which lab you are
working on, and which step you need a hint for with instructor tests not passing.

Once you understand all how this is going to work, you are ready to start coding
the additional functions.


# Step 10: Write an `isString` function and some test cases for it

Here is an example of a function that tests whether something is a list or not.


```
def isList(x):
   """
   returns True if argument is of type list, otherwise False
   """
   
   return ( type(x) == list )   # True if the type of x is a list
```

Your job is to write a similar function that takes a parameter `x` and returns
`True` if `x` is a string (type `str` in Python), and returns `False` if it is
not a string.

Here's a stub for that function.  Add it into your lab03.py file.

```
def isString(x):
   """
   returns True if argument is of type str, otherwise False
   """
   
   return "stub" 


```

And here are three test cases. Add those also:

```
def test_isString_1():
   assert isString("UCSB")

def test_isString_2():
   assert not isString(42)

def test_isString_3():
   assert not isString(["UCSB"])
```

Then, add two more test cases, following the examples above. Those
test cases should be functions named `test_isString_4` and
`test_isString_5`.  One of those should check something that you think
*is* a string, and one more that you think checks something that is
*NOT* a string.   Try to come up with different test cases than the ones given.

Be sure each of your tests cases has a different name.

Finally, go through all the same steps that you did before:

* make sure the file compiles ok
* test with `pytest` and see the tests fail
* fix the function and see the `pytest` tests pass

As a reminder, you can use `-k blah` to run only the tests that have `blah` in their name&mdash;for example, for this step, you'd use:

```
python3 -m pytest lab03.py -k isString
```

Then finally, try submitting to Gradescope and see if you get the credit for the tests for this function. 

# Step 11: Write an `isNumber` function and some test cases for it

Our last function is one called `isNumber` that should take a parameter `x` and return
`True` if the value `x` refers to is either of type `int` or of type `float`.  In any other case, it should return `False`.

You should write the function definition, and you should write exactly five test cases,
with function names:

* `test_isNumber_1`
* `test_isNumber_2`
* `test_isNumber_3`
* `test_isNumber_4`
* `test_isNumber_5`

Follow the model from earlier.

Test your code with:

```
python3 -m pytest lab03.py -k isNumber
```

Then test your code by submitting to Gradescope.

# Step 12: Read over this "countSpaces" function

Here is an example of a function definition for countSpaces along with some test cases.  Copy it into your lab03 file.

Note that this function works correctly as long as we give it a string as its argument.

Below might be the first time you've seen the += operator.  What it does, is that
```
count += 1
```
is logically equivalent to
```
count = count + 1
```
allowing your code to be just a little bit more concise.

```
def countSpaces(someString):
    "return the number of spaces in the string"
    count = 0
    for s in someString:
        if s==" ":
           count += 1
    return count

```

Let's test this interactively.  We can see that it works properly if it give it a string, counting the number of spaces:

```
>>> countSpaces("UC Santa Barbara")
2
>>> countSpaces("UCSB")
0
>>> countSpaces("Cal Poly")
1
>>> countSpaces("UC Davis")
1
>>> countSpaces(" x ")
2
>>> 
```

But, what if we give it something that isn't a string?  In that case, we get some unfortunate results.

```
>>> countSpaces({"school":"UC San Diego"})
0
>>> countSpaces(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 4, in numberOfSpaces
TypeError: 'int' object is not iterable
>>> 
```

The problem is that the numberOfSpaces function expects a parameter of a certain type.  It expects a string (`str` in Python).  If we give it something else, we get an error message that doesn't make much sense (e.g. `'int' object is not iterable`) or an answer that doesnt' make sense (e.g. 0 for "UC San Diego").

In the next step, we'll learn a technique for checking the type of parameters and making sure they are reasonable before we proceed to calculate a result.

# Step 13: Modifying `countSpaces` to check parameter type

To ensure that `countSpaces` gives a more sensible error message when we give it something that isn't a string, 
we can use this Python code:

```
   if (not type(someString)==str):
      raise ValueError('The countSpaces function only works on strings')
```

Add this code into the `countSpaces` function, immediately after the docstring, i.e. right before the line `count = 0`.

Then try running it again with parameters that are not strings, and see if you get results like the ones shown below.

Basically, any time we put in something other than a string, we want to always see the message `ValueError: The countSpaces function only works on strings`.  Otherwise, it computes the correct results for us.

```
>>> countSpaces(3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "lab03.py", line 4, in countSpaces
    raise ValueError('The countSpaces function only works on strings')
ValueError: The countSpaces function only works on strings
>>> countSpaces({"school":"UC San Diego"})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "lab03.py", line 4, in countSpaces
    raise ValueError('The countSpaces function only works on strings')
ValueError: The countSpaces function only works on strings
>>> 
```

# Step 14: Add test cases for `countSpaces`

Here are some test cases for `countSpaces`: add these to your file.

```
def test_countSpaces_1():
  assert countSpaces("UCSB")==0

def test_countSpaces_2():
  assert countSpaces("UC San Diego")==2

def test_countSpaces_3():
  assert countSpaces("Cal Poly")==1

def test_countSpaces_ten_spaces():
  assert countSpaces("          ")==10

def test_countSpaces_space_begin_and_end():
  assert countSpaces(" x ")==2

def test_countSpaces_raises_ValueError_for_int():
  with pytest.raises(ValueError):
    result = countSpaces(3)

def test_countSpaces_raises_ValueError_for_dict():
  with pytest.raises(ValueError):
    result = countSpaces({"school":"UC San Diego"})

```

# Step 15: Add a function `countX`

Now add a definition, and test cases for a function called `countX` that:
* takes one parameter
* checks if that parameter is of type `str`; if it isn't, raises a ValueError with an appropriate message
* counts the number of times the letter X appears.   Both uppercase X and lowercase x should count.

Examples:
* `countX("UCSB") should return 0
* `countX("Fox")` should return 1
* `countX("Xerox")` should return 2
* `countX(3) should raise `ValueError` with an appropriate message indicating that a string was expected

Hint: You may need to use `and` or `or`.  Note that to check whether a string called `s` is `X` or `x`, you must write:

```
if s=='X' or s=='x':
```

If you write the following, it will run, but it doesn't mean what you think it does:

```
if s=='X' or 'x':
```

Write some appropriate test cases.   Your test cases should include both strings with upper and lowercase x, as well as at least one case of an argument that is not a string.   See the test cases for countSpaces for examples.

# Step 16: See 70/100 score on Gradescope; profit.

At this point, you should see that you have a perfect 70/100 points on Gradescope.

That is a perfect score for the automatically graded parts of the lab.   For this lab there is also a manually graded part, where a reader, TA, or instructor will review your code and give a score out of 30.

Here are the items we'll be looking for as we assign those thirty points:

1. (5 pts) Did you add a third test cases for `areaRect` with different values from the other two?
2. (5 pts) Did you add two more test cases for `isString`?
3. (10 pts) Do you have five test cases for `isNumber`?
4. (10 pts) Do you test at least five cases for countX, covering both upper and lower case X, as well as passing a parameter that isn't a string?
