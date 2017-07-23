---
id: 173
title: 'Conflict Resolution in CSS &#8211; Specificity and !important'
date: 2014-08-25T16:37:58+00:00
author: tapananand

guid: http://www.ktreat.com/?p=173
permalink: /conflict-resolution-in-css-specificity-and-important/
custom_total_hits:
  - "000001953"
categories:
  - CSS
  - Web-Development
---
Hello dear readers, so finally I have a blog post on CSS which is also one of  my favorite.  And we&#8217;ll be talking about conflict resolution in CSS. Ever made changes to your CSS and refreshed your page to see no changes at all or some weird changes in colors, etc. Well, this post will tell you to detect the cause for such problems &#8211; conflicts and will tell you the good practices to avoid them.

So, to understand conflict resolution, let&#8217;s first understand the three ways in which you can apply CSS in your document:

  1. #### **Inline CSS:**
    
    This includes the CSS rules you apply within the element itself using the style attribute as follows:
    
        <a href="www.abcd.com" style="color:red; text-decoration:none"></a>

  2. #### **Internal CSS:**
    
    This includes the CSS rules you apply within the **<style>** tag in the **head** element of your page:
    
    <pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;An Example&lt;/title&gt;
&lt;style&gt;
a
{
    text-decoration: none;
    color: red;
}
&lt;/style&gt;
&lt;/head&gt;
&lt;/html&gt;
</pre>

  3. #### **External CSS:**
    
    This includes the CSS rules you apply in an external **.css** file and include it using **<link> tag** in your html.</li> </ol> 
    
    Within these, the order of priority for conflict resolution is: **In-line > Internal ~ External.** Within Internal and External, the one closer to the element is the one that takes effect. So, consider the following code:
    
    <pre>&lt;!doctype html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;meta charset="utf-8"&gt;
&lt;title&gt;Untitled Document&lt;/title&gt;
&lt;style&gt;
p
{
color:blue;
}
&lt;/style&gt;
&lt;link rel="stylesheet" href="style.css"/&gt;
&lt;/head&gt;

&lt;body&gt;
&lt;p id="test"&gt;
This is a test.
&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>
    
    The contents of style.css are:
    
    <pre>p
{
    color:green;
}
</pre>
    
    The final color of p in the above will be green as the link comes after the style tag and is closer to the p element. If you exchange the two you&#8217;ll see that it gets blue.
    
    ### !important
    
    But what if you want to increase importance of a particular style without altering the order. Well you can use the important declaration for this. In the above code, if you want to increase the importance of the blue color rule in the internal CSS you just have to change it to:
    
    <pre>p
{
    color: blue !important;
}
</pre>
    
    And you&#8217;ll see that the output becomes blue now irrespective of the source order. Now even, if you add an inline rule to make the color red, it&#8217;ll still stay blue. But using important is considered bad practice due to following reasons:
    
      1. It makes your code less maintainable, as if you don&#8217;t remember which rules you made important you may not be able to detect later why your rules are not getting applied.
      2. If a user applies <a title="User-Stylesheets" href="http://webdesign.about.com/od/userstylesheets/a/aa010906.htm" target="_blank">user stylesheets</a> it may cause problems as some of user&#8217;s rules may not work.
    
    So, what do you do then. Well, the most preferred way and the best one is to make your selectors more specific by increasing the specificity of your rules.
    
    ### Specificity
    
    So, what is this specificity. Well it&#8217;s a mathematical algorithm applied by your browser to calculate the importance of your rules and hence to resolve conflicts. Every CSS version interprets this algorithm slightly differently. So, how to do you do it? Well, to understand let&#8217;s get the basic idea of how specificity is calculated. Specificity calculation considers the following 4 values:
    
      1. **Styles: **if the selector uses inline style, this is 1 else 0.
      2. **ID&#8217;s: **the number of id&#8217;s in your selector.
      3. **Classes and pseudo-classes:** Number of classes and pseudo-classes (:hover, :link, etc are pseudo-classes) in the selector.
      4. **Tags:** Number of tags in your selector.
    
    The above 4 values are in the decreasing order of their relative weightage. So, ids are more important than classes and so on.
    
    So, for example:
    
    <pre>#parentid p  /* Specificity = 0(not inline)-1(one id test)-0(no classes)-1(one p tag) */
div#parentid p /* Specificity = 0(not inline)-1(one id test)-0(no classes)-2(two tags p and div) */
</pre>
    
    In the above two, the second selector has the higher specificity value.
  
    So, now consider a final set of examples to clarify a bit more. Consider the code we saw above that has a paragraph with id as test. **Remove the style in the head tag.**. Now, consider the style.css file has been changed to this:
    
    <pre>#test
{
	color: green; /* specificity = 0 - 1 - 0 - 0 */
}

p
{
	color: blue; /* specificity = 0 - 0 - 0 - 1 */
}
</pre>
    
    What do you think will be the color this time?? The answer is green even though blue appears afterwards this is because ids(number 2) have more weight than tags(number 4).
  
    Now, if we change style.css to:
    
    <pre>p#test
{
	color: red;
}
#test
{
color: green;
}
p
{
color: blue;
}
</pre>
    
    The color will now be??? &#8230;. red as specificity of the first selector is **0 &#8211; 1 &#8211; 0 &#8211; 1 > 0 &#8211; 1 &#8211; 0 &#8211; 0**.
    
    So, now you know the best way to avoid conflicts in CSS and wondering why your changes aren&#8217;t applying. Its always a good practice to write specific selectors like **p#test** always. **Make it a habit, to avoid confusion later**.
  
    So, that&#8217;s all for today. I hope it was informative. Comment if you have any.
    
    [subscribe2]