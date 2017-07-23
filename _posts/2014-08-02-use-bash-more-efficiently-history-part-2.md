---
id: 101
title: 'Use Bash more efficiently: History &#8211; Part 2'
date: 2014-08-02T17:48:31+00:00
author: tapananand

guid: http://www.ktreat.com/?p=101
permalink: /use-bash-more-efficiently-history-part-2/
custom_total_hits:
  - "000001269"
categories:
  - Linux
---
This post is a sequel to the earlier post: <a href="http://www.ktreat.com/?p=54" target="_blank">Use Bash more efficiently: History &#8211; Part 1</a>, I hope you remember the things I described in it. I recommend just trying out all the commands from the first post on your terminal. **Practically using is more important than knowing.**

### Topics for today:

  1. [More advanced operators.](#AdvOps)
  2. [Modifying the history.](#mod)
  3. [Customizing the history.](#cust)
  4. [Disabling history to execute Secret commands 😉 .](#del)

<a name="AdvOps"></a>

### More Advanced Operators:

<ul type="square">
  <li>
    <h4>
      ? operator :
    </h4>
    
    <p>
      The ? bash history operator is similar to the * wild-card character. Yes, and I didn&#8217;t mistype * here 😛 . Lets see some examples:
    </p>
    
    <pre>$ !da?
</pre>
    
    <p>
      The above command prints and executes the most recent command that starts with <strong>da</strong>, e.g. the date command.
    </p>
    
    <pre>$ !?thread?
</pre>
    
    <p>
      The above command prints and executes the most recent command that has <strong>thread</strong> in it, e.g. compiling a thread program that you did some time ago.</li> 
      
      <li>
        <h4>
          ^ or the quick substitution operator :
        </h4>
        
        <p>
          The ^ bash history operator runs the last command again replacing one string with another. For Example:
        </p>
        
        <pre>$ gcc -fPIC library.c
$ ^-fPIC^-shared</pre>
        
        <p>
          The second command above evaluates to:
        </p>
        
        <pre>gcc -shared library.c</pre>
      </li>
      
      <li>
        <h4>
          The -p option :
        </h4>
        
        <p>
          What if you just want to see what command will be executed if you write a particular history command line but don&#8217;t actually want to execute the command? You can do this using the -p option. For Example:
        </p>
        
        <pre>$ history -p !-2
</pre>
        
        <p>
          The above command <strong>just prints and doesn&#8217;t execute</strong> the second last command.</li> </ul> 
          
          <p>
            <a name="mod"></a>
          </p>
          
          <h3>
            Modifying the history:
          </h3>
          
          <ul type="square">
            <li>
              <h4>
                Deleting an Entry :
              </h4>
              
              <p>
                You can delete a particular numbered entry from your history using the <strong>-d option.</strong> Lets see an example:
              </p>
              
              <p>
                <!--more-->
              </p>
              
              <pre>$ history -d 2000
</pre>
              
              <p>
                The above command simply deletes the 2000 numbered entry from the current history, i.e. before adding this command to the history. Just see the illustration below to understand:
              </p>
              
              <pre>$ history 5
 2016  history
 2017  history -d 2010
 2018  history
 2019  history 10
 2020  history 5
$ history -d 2019
$ history 5
 2017  history -d 2010
 2018  history
 2019  history 5
 2020  history -d 2019
 2021  history 5
$
</pre>
            </li>
            
            <li>
              <h4>
                Adding an Entry :
              </h4>
              
              <p>
                You can add an entry into the history without executing that command using the <strong>-s option.</strong> For Example:
              </p>
              
              <pre>$ history man man
</pre>
              
              <p>
                Adds <em><strong>man man</strong></em> command to history without it getting executed.</li> 
                
                <li>
                  <h4>
                    Playing with the <em><strong>.bash_history</strong></em> file :
                  </h4>
                  
                  <p>
                    Bash stores the history in the <strong>.bash_history</strong> file in your home directory or the file specified by <strong>$HISTFILE </strong>shell variable. Each time we start the bash shell, the history is loaded from this file and each time we exit the shell the history is saved to this file. The maximum size of this file is determined by the shell variable <strong>$HISTFILESIZE</strong>. You can save or load the current history to or from another file using <strong>-w and -r</strong> options respectively.
                  </p>
                  
                  <pre>$ history -w filetowriteto.txt
$ history -r filetoloadfrom.txt
</pre>
                  
                  <p>
                    Also, see:
                  </p>
                  
                  <pre>$ history -a
$ history -n
$ history -c
</pre>
                  
                  <p>
                    The <strong>-a option </strong>appends the current history to the history file. The <strong>-n option </strong>reloads the history from the history file. The <strong>-c option </strong>deletes the entire history.</li> </ul> 
                    
                    <p>
                      <a name="cust"></a>
                    </p>
                    
                    <h3>
                      Customizing the history:
                    </h3>
                    
                    <p>
                      You can customize how history works for you using the <strong>shopt</strong> bash built in command. It allows you to change additional shell optional behavior. Just run shopt on your shell and you will see the current state(on/off) of all the optional shell behaviors.
                    </p>
                    
                    <pre>Usage: shopt [-pqsu] [-o] [optname …]</pre>
                    
                    <p>
                      The most important options are:
                    </p>
                    
                    <ol>
                      <li>
                        <strong>-s </strong>: Enable (set) each <var>optname</var>.
                      </li>
                      <li>
                        <strong>-u : </strong>Disable (unset) each <var>optname</var>.
                      </li>
                      <li>
                        <strong>-o : </strong>Work on special set built in options.
                      </li>
                    </ol>
                    
                    <p>
                      So, to see all the shell options related to history execute the following command:
                    </p>
                    
                    <pre>$ shopt|grep hist
cmdhist        	on
histappend     	on
histreedit     	off
histverify     	off
lithist        	off
</pre>
                    
                    <p>
                      Lets see these one by one:
                    </p>
                    
                    <ol>
                      <li>
                        <strong>histappend : </strong>If this shell option is on, each time we exit our shell the history is appended to the <strong>.bash_history</strong> file.
                      </li>
                      <li>
                        <strong>histverify : </strong>As you have seen so far, whenever we execute a history related command, it immediately gets executed.  What if we want to edit it first and then execute it? You can do this if the <strong>histverify</strong> option is on. But it is off by default, so to enable it do: <pre>$ shopt -s histverify
</pre>
                        
                        <p>
                          Now, try:
                        </p>
                        
                        <pre>$ !-3
$ gcc abc.c (cursor blinking here - not executed yet. Edit and then press enter to execute.)
</pre>
                      </li>
                      
                      <li>
                        <strong>cmdhist : </strong>Saves multiple line commands in the history.
                      </li>
                    </ol>
                    
                    <p>
                      <a name="del"></a>
                    </p>
                    
                    <h3>
                      Disabling history:
                    </h3>
                    
                    <p>
                      So, finally we are going to learn how to disable history, so that all the commands that you execute from now on are not recorded in history. Very handy for doing something nasty isn&#8217;t it 😉 😛 . This is done by turning off one of the shell options which you haven&#8217;t seen yet. Well, see it now:
                    </p>
                    
                    <pre>$ shopt -o | grep hist
history      on
</pre>
                    
                    <p>
                      So just turn this off like this:
                    </p>
                    
                    <pre>$ shopt -u -o history
</pre>
                    
                    <p>
                      And now execute <strong>any</strong> command 😉 , it would not show up in history. And after you are done with your nasty task, don&#8217;t forget to re-enable it so nobody gets to know 😛 .
                    </p>
                    
                    <pre>$ shopt -s -o history
</pre>
                    
                    <p>
                      So that&#8217;s all for the Bash history command. This is a bit longer post but I hope you like it. Please <a href="http://www.ktreat.com/?p=101#respond">comment</a> if you have any suggestions, doubts, etc.
                    </p>
                    
                    <p>
                      Also don&#8217;t forget to subscribe to automatic updates direct to your email, if you haven&#8217;t done that yet, below:
                    </p>
                    
                    <p>
                      [subscribe2]
                    </p>