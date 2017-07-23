---
id: 152
title: 'Use Bash more efficiently: Keyboard Shortcuts'
date: 2014-08-06T16:45:44+00:00
author: tapananand

guid: http://www.ktreat.com/?p=152
permalink: /use-bash-more-efficiently-keyboard-shortcuts/
custom_total_hits:
  - "000001466"
categories:
  - Linux
---
This is a post on Bash Keyboard Shortcuts and if used regularly these passwords will surely lighten your tasks on the Bash shell 🙂 .

But before beginning, you need to understand that, your Bash shell can either run in **emacs mode or the vi mode** and the shortcuts are different for each mode. Mostly the **default mode is emacs** and this post assumes this. But you can check your mode as follows:

<pre>$ shopt -o | grep emacs
$ shopt -o | grep vi
</pre>

Now, if emacs mode is off and vi mode is on, just toggle these as follows(By the way I already taught you <a href="http://www.ktreat.com/?p=101#cust" target="_blank">how to work with shopt</a> in a previous post):

<pre>$ shopt -u -o vi
$ shopt -s -o emacs
</pre>

So having said that lets get started:

<ul type="square">
  <li>
    <strong>Clear the screen: </strong>CTRL + L
  </li>
  <li>
    <strong>Swap the the last two words before the cursor: </strong>CTRL + T<br /> This shortcut can be used to correct a typo, For Example: say you typed <strong>grpe</strong> instead of <strong>grep</strong>, so press Ctrl + T at this position and your typo is corrected.
  </li>
  <li>
    <strong>Swap the last two words before the cursor: </strong>ESC + T<br /> So say, you forgot whether in grep the expression to search for comes first or the filename, so you may use this shortcut like this:</p> <pre>$ grep file pattern
$ grep: pattern: No such file or directory
</pre>
    
    <p>
      Now, use <strong>CTRL + P(or the up arrow key) </strong>to go to the previous command and press <strong>ESC + T </strong> and the words are swapped and it works now.
    </p>
    
    <pre>$ grep pattern file</pre>
  </li>
  
  <li>
    <strong>Cut the word just before the cursor: </strong>CTRL + W. <pre>$ abcd efgh ijkl mnop qrst
$ abcd efgh ijkl mnop (CTRL + W pressed once)
$ abcd efgh ijkl (CTRL + W pressed twice)
</pre>
  </li>
  
  <li>
    <strong>Cut everything after the cursor: </strong>CTRL + K or ALT + D <pre>$ abcdef<strong>g</strong>hijkl (cursor is at g and CTRL + K pressed.)
$ abcdef</pre>
  </li>
  
  <li>
    <strong>Cut the whole line before the cursor: </strong>CTRL + U <pre>$ abcd efgh ijkl mnop qrstu(Cursor here CTRL + U pressed.)
$ (Cursor here)</pre>
  </li>
  
  <li>
    So how do you<strong> Paste what you cut </strong>in the last three shortcuts<strong>?? Not through CTRL + V but: </strong>CTRL + Y &#8211; This by the way is called yanking, therefore the <strong>Y.</strong>
  </li>
  <li>
    Now, what if I told you that<strong> you can UNDO what you typed/edited/etc on the line in Bash? Great isn&#8217;t it: </strong>It&#8217;s easy just use: CTRL + SHIFT + &#8211; or better said as CTRL + _ . Just try it yourself it&#8217;s fun 🙂 .
  </li>
  <li>
    <strong>Toggle between the start of line and current cursor position: </strong>CTRL + XX.
  </li>
  <li>
    <strong>Convert all characters from the cursor to the end of the current word to uppercase: </strong>ALT + U
  </li>
  <li>
    <strong>Convert all characters from the cursor to the end of the current word to lowercase: </strong>ALT + L
  </li>
  <li>
    Of course there is the awesome shortcut for<strong> auto-completion of words/commands:  </strong>TAB.
  </li>
  <li>
    And, don&#8217;t forget to <strong>press tab twice to see all possible hints.</strong>
  </li>
  <li>
    <strong>Move to the beginning of the next word in reverse order on the line: </strong>ALT + B.
  </li>
  <li>
    <strong>Move to the beginning of the current line: </strong>CTRL + A or HOME key.
  </li>
  <li>
    <strong>Move to the end of the current line: </strong>CTRL + E or END key.
  </li>
  <li>
    <strong>Move back one character: </strong>CTRL + B or LEFT arrow key.
  </li>
  <li>
    <strong>Move forward one character: </strong>CTRL + F or RIGHT arrow key.
  </li>
</ul>

So, these are all the cool shortcuts I wanted to tell you about. I hope you liked few of these and will bring into practice using these for more efficiency when working on the Bash shell. Thanks for reading. Comment, if you have any.

[subscribe2]