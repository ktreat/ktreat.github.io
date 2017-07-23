---
id: 159
title: Creating Your Own C/C++ library
date: 2014-08-18T16:58:32+00:00
author: tapananand

guid: http://www.ktreat.com/?p=159
permalink: /creating-your-own-cc-library/
custom_total_hits:
  - "000001466"
categories:
  - C
  - C++
  - Linux
  - Programming
---
Hello, my dear readers. So I&#8217;m back with a brand new post on my blog for you. I understand this is after about two weeks as I was on vacations 🙂 .

So, lets get to the business. Today&#8217;s post is about creating a c/c++ library by yourself and be able to use it like any other standard libraries. But before that we need to understand how libraries work.

A library has two parts:

  1. <h3 style="text-decoration: underline;">
      Header Files:
    </h3>
    
    these files contain just the declarations of all the functions, variables, structs, etc. These files also contain the _**#defines**_ present in the library. On a Linux system, the header files are present in the following directory:
    
    <pre>/usr/include
</pre>
    
    Why don&#8217;t you go ahead and see what&#8217;s present in the most used c header file &#8211; <stdio.h> by executing the following command:
    
    <pre>$ cat /usr/include/stdio.h | less
or
$ gedit /usr/include/stdio.h &
</pre>

  2. <h3 style="text-decoration: underline;">
      Compiled Object files:
    </h3>
    
    these files contain all the definitions of the functions, variables, etc in the library. Generally, there are multiple definition files in a library &#8211; typically one for each function or a set of related functions. These files are all combined into a single file which is the so-called library. Based on this combined file the libraries are of two types:
    
      1. #### Static library:
        
        These libraries are statically linked, i.e. the code for the required function is included in the final compiled file that uses the library. So, if you make a change to the library, you will need to recompile all the codes that used that library for changes to take effect. In Linux, static libraries are archived libraries and have the extension **.a.** Though you will hardly find any on your system, may be some in:
        
        <pre>/usr/lib
$ ls /usr/lib | grep [.]a
</pre>
    
      2. #### Dynamic library:
        
        These libraries are dynamically linked during run time and not added to the compiled unit during compile time. Thus, even if the library changes you don&#8217;t need to re-compile the code. In Linux, dynamic libraries are shared object libraries and have the extension **.so.** You can see these in the following directory:
        
        <pre>$ ls /lib/i386-linux-gnu/
</pre>
        
        **Note:** The second part of the path may vary according to your installation but you will be able to identify &#8211; it&#8217;ll look similar. Just the **i386** part may change.
        
        Now, there is a point I would like to make about the naming of these libraries. Consider the maths library, you include it in your code using **-lm** this means the **.so** file for the maths library will be names like this : **libm.so** or something similar.The **l is expanded to lib** automatically at compile time. Also not the standard c library &#8211; the one referred by the file **<stdio.h>** is named **libc-<version>.so** and is always linked automatically and that&#8217;s why you don&#8217;t require the **-lc** as you would expect during compilation.</li> </ol> </li> </ol> 
        
        So, how do you make a library of your own and use it like other libraries. For example, you may want to put all your fast I/O functions in a library instead of copy pasting each time or may be some other algorithms, etc. Well just go through the steps below:
        
        ### Creating a Static Library
        
        Write a header file which contains just the prototypes of all the functions you are going to use. Name it so that it ends with a .h. Copy it to the **/usr/include** directory:
        
        <pre>$ sudo cp ./mylibrary.h /usr/include
</pre>
        
        Now, compile all the source files for all your functions and put them in a separate directory. Now, **cd** into that directory and execute the following command:
        
        <pre>$ gcc -c *.c
or 
$ gcc -c [list of c files to be included in library...]
</pre>
        
        The **-c** option above just creates the **.o** object files for the **.c** files instead of making the executable. Now, we&#8217;ll create the **.a** archive using the **ar command.** 
        
        <pre>$ ar -rcs libmylibrary.a *.o
or
$ ar -rcs libmylibrary.a [list of .o files created above...]
</pre>
        
        Now, copy the resultant **libmylibrary.a** file to /lib/i386-linux-gnu/:
        
        <pre>$ sudo cp ./libmylibrary.a /lib/i386-linux-gnu/
</pre>
        
        Now, you can use this library in your codes by including the header file **<mylibrary.h>** and compiling your code by using **-lmylibrary** at the end.
        
        ### Creating a Dynamic library:
        
        The header file stuff is the same as above. The only changes are in the compilation:
        
        <pre>$ gcc -c -fPIC [list of .c files...]
</pre>
        
        The **-fPIC** above sets the flag to create **<a href="http://en.wikipedia.org/wiki/Position-independent_code" target="_blank">Position Independent Code</a>** which is required for relocation capability in dynamic libraries. Now we will form the .so file:
        
        <pre>gcc -shared -o libmylibrary.so [list of object files...]
</pre>
        
        Now, copy the **libmylibrary.so** library file to /lib/i386-linux-gnu/:
        
        <pre>$ sudo cp ./libmylibrary.so /lib/i386-linux-gnu/</pre>
        
        Now, you can use this library in your codes by including the header file **<mylibrary.h>** and compiling your code by using **-lmylibrary** at the end.
  
        And that&#8217;s it for today. Hope you liked and needed it. Comment if you have any.