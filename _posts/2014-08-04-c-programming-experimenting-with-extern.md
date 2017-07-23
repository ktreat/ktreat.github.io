---
id: 134
title: 'C Programming: Experimenting with extern'
date: 2014-08-04T15:46:26+00:00
author: tapananand

guid: http://www.ktreat.com/?p=134
permalink: /c-programming-experimenting-with-extern/
custom_total_hits:
  - "000002161"
categories:
  - C
  - Programming
---
So, finally a programming post on  a computer science blog 🙂 . And it is about one of the most dreaded and misunderstood keywords that the founders of C ever produced &#8211; it is about the **extern keyword**. I will try my best to remove the dread and sort out the misunderstanding. So, lets get started then.

To understand the extern keyword, you must first understand the difference between declaration and definition.

### Declaration:

Declaration is a way of making the compiler know that the declared entity(variable/function) does exist and its definition will be found later &#8211; in a separate file, or in the same file, or in a library that will be linked at link time. No memory is allocated to the entity at the time of declaration.

### Definition:

Definition of an entity is what allocates memory for that entity.

### The One Definition Rule(ODR):

The ODR states that a variable or a function can have multiple declarations in a compilation unit but only a single definition &#8211; Can&#8217;t allocate memory twice for the same thing.

So lets see some examples:

<pre>int fun(int, int);</pre>

The above statement simply declares a function named **fun that takes two integer arguments and returns an integer.**

<pre>int fun(int a, int b)
{
    return (a + b);
}
</pre>

The above snippet is the definition of the declared function **fun. **Now consider the statement below:

<pre>int a;
</pre>

The above statement is both, declaration and definition of an integer variable named a. In fact without the use of extern, there is no way you can only declare a variable. So, lets dive into extern now.

When we declare an entity as extern, it can be used across all the files in the program provided a declaration for that is provided in that file.

### **extern** in functions:

In C, all functions are by default extern and thus can be used across files in the program. So, if you declare a function as:

<pre>extern int fun(int, int );</pre>

The extern is redundant.

### **extern** in variables:

This is how you declare a variable as extern:

<pre>extern int a;</pre>

Also note that all global variables are extern by default.

<pre>#include&lt;stdio.h&gt;
extern int a;
int main()
{
    printf("%d\n", a);
    return 0;
}
</pre>

The above program will give linker error as a is not defined or allocated memory yet and we are trying to access it. So, to define **a** write the following outside all functions:

<pre>int a = 5;</pre>

The value 5 is optional and if not given **a** has value 0.

So, now lets see an example:

<pre>#include&lt;stdio.h&gt;
extern int i; //declaration of i.
void fun()
{
	printf("%d\n", i);
}

int main()
{
	extern int i; //declaring that the i main uses is the global(extern) one.
	i++;
	fun();
	return 0;
}
int i = 5; //definition and initialization of i.
</pre>

The output of the above program will be **6**, since i++ works on the global i.
  
But if we remove the extern from the first line in main, the output will be 5, as i++ will then work on the local i.

Now, consider the following code:

<pre>#include&lt;stdio.h&gt;
extern int a = 5;
int main()
{
    printf("%d\n", a);
    return 0;
}
</pre>

The above program works just fine without any error and prints 5. Why?? Well according to the C standard:

> We can provide an initializer on a variable defined as extern. An extern that has an initializer is a definition. **It is an error to provide an initializer on an extern inside a function**.

So, the first two sentences explain why the above code works. But, what about the sentence in bold. It says that if we write the extern line inside main instead of outside, it will give error. Well, this does make sense to not allow extern inside any function. Lets see an example to clarify that:

<pre>#include&lt;stdio.h&gt;
extern int i;
void fun()
{
	extern int i = 10; //line 1
	printf("%d\n", i);
}

int main()
{
	extern int i;
	i++;
	fun();
	return 0;
}
int i = 5;
</pre>

In the above code, had **line 1** in fun not been an error, then what should have been the output?? 6 or 10. Is **i** defined twice?? So, you see there is no way to make sense of this and hence extern should always be globally defined variables.

So, now lets experiment with extern a bit to understand it deeper:
  
Consider the following code:

<pre>#include&lt;stdio.h&gt;
extern int i;

int main()
{
	int i = 2;
	printf("%d\n", i);
	return 0;
}
int i = 5;
</pre>

The above program is quite simple and prints the local i&#8217;s value i.e. 2. But what if you want the global value in main?? The solution is written below:

<pre>#include&lt;stdio.h&gt;
extern int i;

int main()
{
	int i = 2;
        printf("%d\n", i);
	{
		extern int i;
		printf("%d\n", i);
	}
        printf("%d\n", i);
	return 0;
}
int i = 5;
</pre>

The above program prints **2, then 5 and then 2. **The line extern int i, brings the extern i into scope for the block inside main. Outside the curly braces though, the **i** is still the local one.

So, I hope I was able to clarify extern to you people, at least a little bit through this post. Thank you for reading, comment if you want to say something. And also once again, below is the form to subscribe to updates via mail.

[subscribe2]