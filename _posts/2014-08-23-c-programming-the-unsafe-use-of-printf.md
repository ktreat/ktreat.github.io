---
id: 165
title: 'C Programming: The Unsafe form of printf'
date: 2014-08-23T16:51:53+00:00
author: tapananand

guid: http://www.ktreat.com/?p=165
permalink: /c-programming-the-unsafe-use-of-printf/
custom_total_hits:
  - "000002850"
categories:
  - C
  - Programming
---
So, here is a post for the C programmers showing them a way to use the **printf** function. So, let&#8217;s start with the prototype of **printf** function

<pre>int printf(const char *format, ...);</pre>

So, the first argument can be a **pointer to constant char** i.e a C string. We usually hard code this first argument as a string literal enclosed within double quotes. The three dots &#8230; are called ellipsis and denote variable number of arguments.

So, what if we don&#8217;t hard code the first argument to **printf**? What if we use it to create an **Error** function allowing to print Custom Error Messages just like below? :

<pre>void Error(char* s)
{
    printf(s);
}
</pre>

The above code will compile and will run just Ok but it will give the following warning during compilation:

<pre>warning: format not a string literal and no format arguments [-Wformat-security]
</pre>

**Beware: **This is not a warning to be ignored. You can also see **-Wformat-security** which means this is a warning pertaining to security. On  a side-note : you should not ignore any warning during compilation specially in a production code.

The reason for this warning is explained below:

The printf function uses the variable argument **stdarg** **c library.** Although this library allows you to take variable number of arguments into a function but when accessing these arguments internally, you need to know the number and types of each. The C compiler can determine the number and types of arguments if the first argument to printf is a hard-coded string literal like **&#8220;Your name is %s\n&#8221;.** 

But if we use printf as we&#8217;ve used in the printf function above, the **char* s** can be pointing to a string that can change during run time and thus compiler can&#8217;t verify the number and types of arguments. This gets even dangerous security wise when user input is involved as nothing is stopping this function from being used like this:

<pre>scanf("%s", str);
Error(str;)
</pre>

Here, a malicious user can provide a malicious string as input which can either crash your program or may lead to very hard to detect bugs. Let&#8217;s look at one such malicious string:

<pre>Hello %n World!%n\n
</pre>

To understand you need to recall what the %n format specifier does. The %n format specifier take the number of characters printed in the current printf so far and puts at the address provided as the argument, so for example:

<pre>int a = 1;
printf("Hello %n\n", &a);
</pre>

After the completion of above printf statement the value of a is 6, as 6 characters were printed before the %n.
  
There is another thing that you should remember about functions is that if you provide lesser arguments in the function call it will take a value from the stack. The reason for this can be understood by exploring the function call stack operations. [Read this](http://www.eventhelix.com/realtimemantra/basics/CToAssemblyTranslation.htm#.U_jBh2OvMgZ) if you are interested in the details.
  
So, now we are ready to see why the above string is dangerous. Consider the following program that uses a function similar to our Error function:

<pre>#include&lt;stdio.h&gt;

void func(const char* s)
{
	int a = 0, b = 1;
	printf("%p %p\n, ", &a, &b);
	printf(s); //call 2
	printf("%d %d\n", a, b);
}

int main()
{
	char s[100];
	fgets(s, 100, stdin);
	func(s);
	return 0;
}
</pre>

Now here, the **call 2 **to printf is dangerous. Suppose the user inputs the above malicious string: **Hello %n World!%n**. It will take the addresses of a and b from the stack and will change them to 6 and 13 respectively. It can also give **segmentation fault** if the values on stack are not retained for security purposes by the Operating System. So, in that case it will crash your program. Now suppose **a** was also inputted from the user or was somehow under his control and if **a** contained the address of some sensitive data, the data could be modified.

So, you see how dangerous can this way of using printf can be and thus should be avoided. Also, don&#8217;t ever ignore any warnings you get during compilation try to understand why you are getting it. For example, the warning when using the gets function is also important security wise due to buffer overflow attacks.

So, that&#8217;s all for today. Hope you liked it. Comment if you have any.

[subscribe2]