---
id: 161
title: 'Programming: Optimizing through switch-case, the internals'
date: 2014-08-21T16:11:25+00:00
author: tapananand

guid: http://www.ktreat.com/?p=161
permalink: /programming-optimizing-through-switch-case-the-internals/
custom_total_hits:
  - "000001026"
categories:
  - C
  - C++
  - Programming
---
Hello everyone, here is the next treat for you and it&#8217;s related to programming. In this post you&#8217;ll learn why switch case is faster than if-else ladder and we&#8217;ll look at an approximate assembly code generated for it. And then finally we&#8217;ll end up with some tricks to write switch case that work quickly. Although these optimizations may not be significant enough for normal systems, but these are very important for real time applications like Embedded systems.

So, let&#8217;s consider the following switch statement:

<pre>switch(num)
{
    case 4: //some code here
            break;
    case 5: //some code here
            break;
    case 6: //some code here
            break;
    case 7: //some code here
            break;
}</pre>

Since, the case values are in a small range the compiler creates a table called **a jump table** which consists of the addresses of the code written inside each case label. As the values are in a narrow range, the compiler can map the value on which switch is to be done into indexes in the **jump table **and thus execute the appropriate function. Let&#8217;s see an assembly code which is something similar to the actual (actually it is a bit compiler dependent and also we are ignoring the default label.) :

<pre>jmp findAddr
case4label: //the assembly for the code under case 4.
       jmp afterSwitch
case5label: //the assembly for the code under case 5.
       jmp afterSwitch
case6label: //the assembly for the code under case 6.
       jmp afterSwitch
case7label: //the assembly for the code under case 7.
       jmp afterSwitch

jumptable: 
db case4label // define a 4 byte value containing the address of case4label
db case5label // define a 4 byte value containing the address of case5label
db case6label // define a 4 byte value containing the address of case6label
db case7label // define a 4 byte value containing the address of case7label

findAddr:
mov _num, R0
sub $4, R0 //subtract the lowest value from the switch value to change to index into jump table.
mov jumptable, R1 //move the address of jumptable to R1
lshift $2, R0 //multiply the index into jump table by 4 to get offset into the table.
jmp (R2, R0) //Jump to R0 + R2 address

afterSwitch:
//more code after switch here...</pre>

So, you see instead of the if-else ladder which take **O(n) time** to match cases (n = number of case values), switch case does it in **O(1) always.**

But what if the values are in  a wide range, for example: if the case values were 1, 2, 8, 2048, 8196. Well in this case the jump table would be very big and sparingly filled. That would have been inefficient and in this case the switch case works just like if-else ladder and is not efficient enough. So, we learn the following lessons from this which can act as guidelines for us when we write switch case specially in  a production code or one for real-time applications:

  1. Try to keep case labels in a narrow and almost continuous range so that a jump table approach can be used without much wasted space(a dense table can be constructed).
  2. If the case labels have to be in a wide and sparse range then try putting the frequently occurring cases first so that they match early in the if-else ladder approach used by compiler.
  3. Some compilers need not put case labels in the same order that they appeared in your code, so to be safe in point 2 above, write switch cases as depicted below: 
    <pre>switch(num)
{
    case frequentcase1: ...
                       break;
    case frequentcase2: ...
                       break;
    ...
    case frequentcasen: ...
                       break;
    default:
            switch(num)
            {
                case infrequentcase1: ...
                       break;
                case infrequentcase2: ...
                       break;
                ...
                case infrequentcasen: ...
                       break;
                default: ...
            }
}
</pre>
    
    So, as you can see we have made the compiler to put our frequent case first and then infrequent ones as the defaults code will always go to the last of the if-else ladder i.e in the else part.</li> </ol> 
    
    So, that&#8217;s all for today. I hope you like it. If anything is not clear please comment and ask. Thanks for reading 🙂 .
    
    [subscribe2]