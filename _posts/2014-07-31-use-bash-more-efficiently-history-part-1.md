---
id: 54
title: 'Use Bash more efficiently: History &#8211; Part 1'
date: 2014-07-31T17:04:23+00:00
author: tapananand

guid: http://www.ktreat.com/?p=54
permalink: /use-bash-more-efficiently-history-part-1/
custom_total_hits:
  - "000002011"
categories:
  - Linux
---
So here is a treat from linux side 🙂 and it&#8217;s about using the bash shell more efficiently by using the many facilities that the history command provides.

So, let&#8217;s start with the basics:

<pre>$ history</pre>

The above command simply prints the last N commands you executed, where N = the value of shell variable _**$HISTSIZE**_
  
So, now u know how to change the length of history just append

<pre>export $HISTSIZE=&lt;your value&gt;</pre>

in your **.bashrc** file. Strive for infinite history or zero history for the naughty ones 😛 . Don&#8217;t worry i&#8217;ll also tell how to disable history in a later post 😛 .

<pre>$ history 10</pre>

The above command simply prints the last 10 commands you executed. You can change 10 to any number. And for those you testers out there do test what if value you type is greater than $HISTSIZE.

But now, things get interesting with the introduction of **! operator.**

**! **denotes start of a command to be completed by bash.

Examples:

<pre>$ !!</pre>

Prints and executes the last command.

<pre>$ !N</pre>

where N is any number; prints and executes the command preceeded by number N in the output of your history command.

<pre>$ !-N</pre>

where N is any number; prints and executes the Nth last command you executed.

And now the next one is very interesting, it&#8217;s

<!--more-->

<pre>$ date; !#</pre>

What !# does is just repeats what is on the left of it. So the above command expands to:

<pre>$ date; date;</pre>

So date is printed twice.
  
But be careful, this has exponential effect 😐 , i.e

<pre>$ date; !# !#</pre>

prints date 4 times and not three times. Since _**date; !#**_ expands to _**date; date; !#**_ and then _**!#**_ repeats it.

So now you know that printing date 1024 times is not a looping problem but a &#8220;**bang hash**&#8221; cakewalk 😛 . Why not try it yourself.

The next one is very useful for all the programmers out there and it is **!$**. **!$** simply substitutes the second argument to the previous command, see below:

<pre>$ make programname
$ ./!$
</pre>

The above compiles the program named **_programname.c_** and then runs it. Handy isn&#8217;t it 🙂 . You can always think of more uses for **!$.**

Next one is even more interesting. We are going to search history now 😐 . Just press Ctrl + R at your prompt. You will get a new prompt like this:

<pre>(reverse-i-search)`':</pre>

Now at this prompt type any word and you will be shown the most recent command having that word as substring.

For example:

<pre>(reverse-i-search)`gcc': gcc semaphore.c -o semaphore -lpthread
</pre>

**Press Enter** to execute the command or **Ctrl+R** to go to older commands containing that as substring. You can also press **Ctrl+O** when a command is shown to execute the current one and move to the next one.

So, that&#8217;s all for this time. I&#8217;ll do at least one more post on history in the future to talk about more advanced operators and customizing **shopt** command.

**Please comment if you like it or have any suggestions or doubts.**