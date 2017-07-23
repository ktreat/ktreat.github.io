---
id: 270
title: 'How a function is called in C : The Internals'
date: 2015-01-06T18:31:05+00:00
author: crisron

guid: http://www.ktreat.com/?p=270
permalink: /how-a-function-is-called-in-c-the-internals/
custom_total_hits:
  - "000001534"
categories:
  - Assembly Language
  - C
  - Programming
---
Hello all! Here&#8217;s my first post (notice the name above) on Ktreat. In this post, we are going to talk about the standard calling convention used by GCC for C functions. But, to understand that we first have to dive into the concept of the system stack. Note that we are assuming a 32-bit Linux system with a 32-bit intel processor (the x86 architecture).

<pre style="text-align: center;">mov a, b implies move value of a into b</pre>

### The System Stack

The x86 architecture uses a stack as a temporary storage area in RAM. This stack functions just like the standard data structure stack. However, there are some points about the system stack which need to be kept in mind:

  1. The top of the stack is pointed to by the **esp** register.
  2. The stack **grows downward** i.e. from high to low memory address.
  3. When a value is popped off the stack, it remains there until overwritten (may depend on the Operating System). However, some other process may overwrite this value. So, the memory content below esp can&#8217;t be relied upon.

An interesting point to note is that the <a title="Blue Screen Of Death" href="https://en.wikipedia.org/wiki/Blue_Screen_of_Death" target="_blank"><strong>Blue Screen Of Death</strong></a> in Windows is sometimes caused because of **stack overflow** in a device driver or the kernel.

### Pushing on the Stack

Whenever a value(say, the value in **eax** register) is to be pushed on the stack, the following instruction is executed:

<pre>push %eax		;pushes the value in eax register onto the stack</pre>

This is equivalent to the following:

<pre>sub  $0x4, %esp		;decrement esp by 4 bytes (each register is 4 bytes on x86 architecture)
movl %eax, (%esp)	;store the value of eax at the location pointed to by esp</pre>

### Popping from the Stack

Whenever a value is to be popped off(say into the **eax** register) the stack, the following instruction is executed:

<pre>pop %eax		;pops the value from the top of the stack into eax register</pre>

This is equivalent to the following:

<pre>movl (%esp), %eax	;store the value at the top of the stack into eax register
add  $0x4, %esp		;increment esp by 4 bytes
</pre>

### Stack Frames

Functions often set up something called as stack frame. This is done in order to facilitate access to the function parameters and local variables. Some important things to note about stack frames:

  1. Each function in a program sets up its own stack frame independently.
  2. Each function (while it is executing) acts as if it is the current top of the stack
  3. When a function is called, its stack frame is created at the top of the stack.
  4. Each function&#8217;s stack frame creates a partition on the stack **expected** for its use only.
  5. The current function always has access to the top of the stack via **esp**.

We&#8217;ll see in a while how a stack frame is set up.

### Calling Convention

Calling convention governs the method that a compiler uses to set up a stack frame, how are arguments passed (right-to-left or left-to-right), who cleans the stack (calling function or called function) etc. The convention used on a system depends on the <a title="Application Binary Interface" href="http://en.wikipedia.org/wiki/Application_binary_interface" target="_blank">Application Binary Interface (ABI)</a> used on the system.

### C Calling Conventions

The C language uses **CDECL** calling convention by default. Though there are other calling conventions too like **STDCALL** (standard calling convention for the WIN32 API) and **FASTCALL** (used where speed is required). In this post we are going to limit ourselves to the discussion of the **CDECL** convention only.

### CDECL

The **CDECL** calling convention has these properties:

  1. Arguments are passed on the stack in Right-to-Left order (i.e. the last argument is pushed first and the first argument is pushed last.)
  2. Return value is passed in **eax** (Integer values and memory addresses &#8211; may not be true for floating point values). For returning larger structures, a combination of registers may be used. For even larger values, the structure may be returned as an address in memory.
  3. The calling function cleans the stack. (For this reason, CDECL functions can have variable number of arguments)

Let us now look at a simple example and understand the above concepts a bit clearly (Note that we are considering optimizations to be turned off. The actual assembly code might be a bit different).

Consider the following C program (**add.c**):

<pre>#include&lt;stdio.h&gt;
int fun(int a, int b)
{
    int c;
    c = a + b;
    return c;
}
int main()
{
    int x;
    x = fun(1, 2);
    return 0;
}
</pre>

Compile the above program using:

<pre>gcc add.c -o add</pre>

To disassemble the executable produced or to see its assembly code, run the following:

<pre>objdump -d add</pre>

The call to the function( _**x = fun(1, 2)**_ ) generates the following assembly code:

<pre>push $0x2
push $0x1
call [address of fun]  &lt;fun&gt;
add $0x8, %esp
</pre>

The call statement actually does these two things:

<pre>push %eip + $constant ;push return address
jmp _fun</pre>

The **eip** register points to the current instruction being executed. **$constant** is some constant value representing the size of 2 instructions. So, their sum gives the return address (the address on from which execution is resumed after returning from fun). This has been shown below:

<pre>eip ---&gt;| push instruction |addr1     eip = addr1
        | jump instruction |addr2
        |                  |addr3     Return address = addr3
</pre>

At this point, stack looks like this (The addresses shown for the stack are for demonstration purposes only):

<pre>|       b = 2      |988
	|       a = 1      |984
esp ---&gt;|  Return address  |980       esp = 980
</pre>

Now, execution jumps to the first instruction of the function fun. The assembly code produced for fun is:

<pre>push %ebp
mov %esp, %ebp
sub $0x10, %esp
mov 0xc(%ebp), %eax
mov 0x8(%ebp), %edx
add %edx, %eax
mov %eax, -0x4(%ebp)
mov -0x4(%ebp), %eax
leave
ret
</pre>

OMG!! 😯 That looks like eerie writing. But let&#8217;s not dread from it 🙂 . We will now explore each of the above statements and see how does the function operate with the help of stack.

<pre>push %ebp</pre>

**ebp** is always adjusted according to the current function frame. So, it is also called frame pointer. It is used to access the local variables and arguments of a function with which it is currently associated. Here, **ebp** is pushed on the stack. This **ebp** is the frame pointer for the function which must have called fun() i.e. main(). So, stack now becomes:

<pre>|       b = 2      |988
	|       a = 1      |984
	|  Return address  |980
esp ---&gt;|    old ebp       |976		esp = 976
</pre>

<pre>mov %esp, %ebp</pre>

We now set **ebp** so as to access local variables and arguments of current function fun().

<pre>|       b = 2      |988
	|       a = 1      |984
	|  Return address  |980
esp ---&gt;|      old ebp     |976&lt;---ebp		esp = ebp = 976
</pre>

Next, we have to make space for the local variables. This is done by the following instruction:

<pre>sub 0x10, %esp</pre>

It says that decrement **esp** by 16 bytes. We know that we only have a 4 byte local variable inside the function then why does the compiler allocate 16 bytes on the stack? This thing is called stack alignment and is done for performance issues(e.g. &#8211; speed up).

<pre>|       b = 2      |988
	|       a = 1      |984
	|  Return address  |980
	|      old ebp     |976
        |                  |960			esp = 960
</pre>

<pre>mov 0xc(%ebp), %eax
</pre>

This instruction fetches the value at address **ebp+12** i.e. the value of parameter b and stores it in register **eax**.

<pre>mov 0x8(%ebp),%edx</pre>

This instruction fetches the value at address **ebp+8** i.e. the value of parameter a and stores it in register **edx**.

<pre>add %edx, %eax</pre>

It adds the value of both registers (performs a + b) and stores the result in **eax**.

<pre>mov %eax, -0x4(%ebp)</pre>

The **sub** instruction created space of 16 bytes. That space is used to store values of local variables and any temporary variables(if used by the compiler). So, this space is used to store c. Variable c uses the space at **ebp-4** and the value of **eax** is copied there. Until this point, instruction **c = a + b;** is executed_._

<pre>|       b = 2      |988
	|       a = 1      |984
	|  Return address  |980
	|      old ebp     |976&lt;---ebp		ebp = 976
        |       c = 3      |972
        |                  |968
        |                  |964
esp ---&gt;|                  |960			esp = 960
</pre>

<pre>mov -0x4(%ebp), %eax</pre>

This instruction moves the value at **ebp-4** into **eax**. But wait, doesn&#8217;t **eax** already contain that value? 😕 Yes, it does but there are two reasons for the compiler to show this inefficient behavior:

  1. Remember that we were returning c from fun(). Since, in **CDECL**, return value of function is passed in **eax**, the compiler must write an instruction to do that.
  2. While compiling this program, we did not use any optimizations.

Moving on to the next instruction,

<pre>leave
</pre>

This instruction is equivalent to the following two instructions:

<pre>mov %ebp, %esp
pop %ebp
</pre>

Let&#8217;s look at each of them separately:

<pre>mov %ebp, %esp</pre>

This instruction releases the part of the stack frame used by the current function for local variables (in this case, variable c in fun()). However, the values in this portion of stack are still there until overwritten (Some Operating Systems may clear this region for security purposes).

<pre>|       b = 2      |988
	|       a = 1      |984
	|  Return address  |980
esp ---&gt;|      old ebp     |976&lt;---ebp		ebp = esp = 976
        |       c = 3      |972&lt;---Value of c is still there, until overwritten
        |                  |968
        |                  |964
	|                  |960	
</pre>

<pre>ret
</pre>

This is equivalent to the following two instructions:

<pre>pop %eax
jmp *%eax
</pre>

_**pop %eax**_ causes the return address to be popped into the **eax** register. The **jmp** instruction then causes a jump to that return address and the execution resumes from the next instruction after the call instruction in the main function.

<pre>|       b = 2      |988
	|       a = 1      |984
esp ---&gt;|  Return address  |980
	|      old ebp     |976		ebp = old ebp (ebp for main), esp = 988
        |       c = 3      |972
        |                  |968
        |                  |964
	|                  |960	
</pre>

Recall that we talked about cleaning the stack above. What does it mean to clean the stack? Remember that the instruction after the call instruction was:

<pre>add $0x8, %esp
</pre>

This instruction takes **esp** to the address 992 i.e. above the function parameters. This is what exactly cleaning the stack means. The stack frame of the called function fun() is no longer accessible (yes, it looks like it is still there but the values might have been overwritten by now!!). Also note that this **add** instruction was executed by main() i.e. the calling function which verifies the fact that in CDECL calling convention, calling function cleans the stack.

This knowledge of stack frame set up can be put to use in reverse engineering practices 😀 and is a must know for every aspiring reverse engineer and system programmer out there.
  
Hope you enjoyed this interesting post 🙂 . Stay tuned for more!! 🙂
  
Post your reviews in comments below.