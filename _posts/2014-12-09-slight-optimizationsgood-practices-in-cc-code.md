---
id: 244
title: Slight Optimizations/Good Practices in C/C++ code
date: 2014-12-09T07:14:12+00:00
author: tapananand

guid: http://www.ktreat.com/?p=244
permalink: /slight-optimizationsgood-practices-in-cc-code/
custom_total_hits:
  - "000001487"
categories:
  - C
  - C++
  - Programming
---
Welcome back dear readers, here is another treat for you. This one is related to optimizations/best practices in C/C++ code. The optimizations here are not much significant for modern personal computers/laptops. But these can be crucial in case of real time embedded systems and in case of low memory devices. But even if they don&#8217;t provide noticeable effects in case of powerful computers they still are good practices to follow while writing C/C++ code even for these devices. So, lets get started.

<ul type="square">
  <li>
    <h3>
      Limit the number of parameters to a function
    </h3>
    
    <p>
      The number of parameters you pass to a function affects the efficiency of your code. Whenever you call a function, its parameters are to be pushed on the stack. This adds overhead if there are a lot of parameters to be pushed.
    </p>
    
    <p>
      Also, avoid passing structures as parameters instead just pass their <em><strong>pointers or references</strong></em>. This is to be done to avoid large structures to be pushed on the stack. A single structure may require multiple push statements.
    </p>
    
    <p>
      In case of object parameters in C++, copy constructor is called adding a lot of overhead. So, it is better to pass objects as <em><strong>const references</strong></em> to functions.</li> 
      
      <li>
        <h3>
          Limit the number of local variables used inside a function
        </h3>
        
        <p>
          Just like arguments are pushed on to the stack, local variables are also stored on the stack frame of the called function and space is to be allocated for them. Then to access these local variables and parameters of the function offsets from a register called the frame register are used (<a title="Frame Pointer Operations in a C Function Call" href="http://www.eventhelix.com/realtimemantra/basics/CToAssemblyTranslation.htm#.VIaL7BYsGXg" target="_blank">How a function is called in C?</a>). This adds a lot of overhead.
        </p>
        
        <p>
          To avoid these overheads, you can minimize the number of local variables you use. This allows compiler to store the local variables inside a CPU register instead of setting up the frame pointer.</li> 
          
          <li>
            <h3>
              Adjust <em><strong>struct</strong></em> sizes to power of two
            </h3>
            
            <p>
              In case of <em><strong>struct</strong></em> arrays, indexing is to be performed to access each member. If the sizes of <em><strong>struct</strong></em> are in power of 2, then indexing becomes a shift operation, which is quite easy for the CPU.</li> 
              
              <li>
                <h3>
                  Use case labels in narrow range and put frequent cases first
                </h3>
                
                <p>
                  Refer to <a title="Programming: Optimizing through switch-case, the internals" href="http://www.ktreat.com/?p=161" target="_blank">this older post for more details on this and how switch case is converted to assembly</a>.</li> 
                  
                  <li>
                    <h3>
                      Use <em><strong>int</strong></em> instead of <em><strong>char</strong></em> and <em><strong>short</strong></em>
                    </h3>
                    
                    <p>
                      Many programmers tend to use <em><strong>char</strong></em> and <em><strong>short</strong></em> for their variables that take smaller values, thinking that it saves space. But actually it is not always the case. Your memory may be aligned to 32 bits (4 bytes) and hence even <em><strong>char</strong></em> and <em><strong>short</strong></em> may be stored in 4 bytes. Therefore, the space may not always be saved.
                    </p>
                    
                    <p>
                      Secondly, the operations on <em><strong>char</strong></em> and <em><strong>short</strong></em>, like addition, multiplication, etc, are performed by first converting them to <em><strong>int</strong></em> values (Read <a title="Integer Promotions in C" href="http://www.geeksforgeeks.org/integer-promotions-in-c/" target="_blank">more about integer promotion</a>). So, this may also add some overhead to convert to <em><strong>int</strong></em> and then back to the original type.</li> 
                      
                      <li>
                        <h3>
                          Constructors should be short and simple
                        </h3>
                        
                        <p>
                          Another good practice is to keep your constructors lightweight. Avoid doing too many things inside a constructor. The constructors are called at a lot of places, when creating/copying objects, returning objects, for temporary objects, etc. In case of arrays they are called separately for each element. So, avoid doing too many things inside a constructor.</li> 
                          
                          <li>
                            <h3>
                              Use constructor initialization lists
                            </h3>
                            
                            <p>
                              In case of classes that have objects of other classes as their members, it is better to initialize these members by calling their respective constructors in the initialization list of the class&#8217; constructor. This avoids extra overhead of initializing the object members of the containing class inside the constructor because constructors for the member objects are called anyways.</li> 
                              
                              <li>
                                <h3>
                                  Inline functions
                                </h3>
                                
                                <p>
                                  Using  inline functions avoids the overhead of calling the function thus improving efficiency. Inline function calling is equivalent to including the function&#8217;s code at the place of calling. But there are a few things that one must keep in mind when making functions inline.
                                </p>
                                
                                <ul>
                                  <li>
                                    Only inline short functions. If we make long functions inline it causes <a title="Code bloat" href="http://en.wikipedia.org/wiki/Code_bloat" target="_blank">code bloating</a>.
                                  </li>
                                  <li>
                                    Also don&#8217;t inline frequently called functions even if they are short due to the same reason above.
                                  </li>
                                </ul>
                              </li></ul> 
                              
                              <p>
                                So, that&#8217;s all for this post. Hope you liked it. Comment below if you have anything to say.
                              </p>