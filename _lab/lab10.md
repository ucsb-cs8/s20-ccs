---
assigned: 2020-03-11 12:30
csxx: cs20
desc: Review for Final (optional)
due: 2020-03-14 17:00
layout: lab
num: lab10
ready: true
---

This lab is a review of concepts from the course so far.  In College of Engineering offerings of this
course, this would also be a preparation for the final exam.  In CCS, we are not having an exam, but if we 
were, this would be how to study for it.  

## This lab may be done solo, or in pairs.

Before you begin working on the lab, please decide if you will work solo or with a partner.

* You MUST add your partner on Gradescope when submitting your work <strong>*<u>EACH TIME</u>*</strong> you submit a file(s). After uploading your file(s) on Gradescope, there is a "Group Members" link at the bottom (or "Add Group Member" under "Groups") where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on "Group Members" -> "Add Member" and select your partner from the list.

Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

# Instructions

In this lab, you will need to create two files:
* <tt>{{page.num}}.py</tt> - file containing function definitions
* <tt>{{page.num}}_tests.py</tt> - file containing test cases.  You are encouraged (though not required) to write 3 - 5 (or more) additional tests per function to confirm your code works as expected.  This will not be checked by the grader, but it is good practice for the final exam---you will be expected to know how to write test cases on the final exam.   You can see for yourself whether your test cases are working.
* <strong>Please add a comment with you and your partner's name (if applicable) at the top of each file.</strong>

Starter code is provided for you and is located at the files below (you may need to refresh the page if the links do not load immediately):

* [{{page.num}}.py](https://github.com/ucsb-cs8/s20-ccs/blob/master/_lab/lab10/lab10.py)
* [{{page.num}}\_tests.py](https://github.com/ucsb-cs8/s20-ccs/blob/master/_lab/lab10/lab10_tests.py)

For most of the functions the started code and the tests will be enough for you to know what code you are supposed to write.

For the function midi2freq, some additional explanation, provided below, will be needed.

You will complete the portions in the starter code by doing the following:

1.  Create a directory called <tt>~/{{page.csxx}}/{{page.num}}</tt> (using the `mkdir` command) and `cd` into that directory.
2.  Use `idle3` (you might try `idle3 &` if you want to be able to type commands on your terminal window after IDLE opens).
3.  Use "New File" to create empty files called `{{page.num}}.py` and `{{page.num}}_student_tests.py` in that `~/cs8/{{page.num}}` directory.
4.  ONE AT A TIME, copy the function definitions from the starter code, write tests that go along with those functions in `{{page.num}}_tests.py`, and get your tests to pass.
   * Before you move on to the next function definition and <em>its</em> tests, get all of the tests you just wrote to pass.
   * Repeat this until you have ALL of the function definitions and their tests, and all of them pass.

You are encouraged to try submitting to Gradescope periodically for several reasons:

* You can get partial credit if some of your tests pass for some of your functions.
* You will have a backup of your file in case you accidentally delete yours, or in case your laptop dies.
* You can move code between your laptop and CSIL by downloading your submitted code from Gradescope

# Explanation of `midi2freq`

For electronic musical instruments (for example, keyboards), each key on the keyboard is assigned a particular "midi number", an integer corresponding to the numbers on the illustration shown here: 

![midi chart](piano-to-midi.png)

<div style="font-size:80%;" markdown="1">
(adapted from an [article by Joe Wolfe, University of New South Wales](https://newt.phys.unsw.edu.au/jw/notes.html))
</div>

Each note on an instrument has a certain frequency, with notes to the right having higher frequencies, and notes to the left having lower frequencies.   When instruments are tuned in the usual way&#x2a;, the formula to convert from a midi number <em>m</em> to a frequency <em>f</em> is expressed as follows in math notation:

$$ f = (440)(2^{\frac{m-69}{12}}) $$

Your job when writing the definition for `midi2freq` is to write a Python function that computes this value.   This formula is value when $m$ is an integer between 0 and 127 (inclusive).

<div style="font-size:80%;" markdown="1">
&#x2a; For the music geeks, A=440Hz, equal temperament.
</div>


# Upload `{{page.num}}.py` and `{{page.num}}_tests.py` to Gradescope.

Once you're done with writing your functions, navigate to the Lab assignment {{page.num}} on Gradescope and upload your `{{page.num}}.py` and `{{page.num}}_tests.py` files. 

<strong>*Remember to add your name, and your partner to Groups Members for this submission on Gradescope if applicable.  At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and see if you can see the uploaded files for {{page.num}}.*</strong>
