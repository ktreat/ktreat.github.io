---
id: 358
title: 'How to use XChat : An IRC Client'
date: 2015-01-20T15:01:50+00:00
author: crisron

guid: http://www.ktreat.com/?p=358
permalink: /how-to-use-xchat-an-irc-client/
custom_total_hits:
  - "000003383"
categories:
  - Open Source
---
Hello dear readers! In today&#8217;s post we will learn about an Internet Relay Chat(IRC) client &#8211; XChat. Whenever we use any software, we use it for some specific application. To understand the utility of XChat, we first must know about <a title="open source" href="http://opensource.com/resources/what-open-source" target="_blank">open source</a>. Quoting directly from the linked article,

> The term &#8220;Open Source&#8221; refers to something that can be modified because its design is publicly accessible

Talking about open source software, Linux is the biggest open source project ever developed in computing history. Linux is open source while Windows, MacOS and UNIX are not. That means you can modify the design of the Linux operating system because its source code is publicly available. But, modifying the source code of an operating system(or any other open source software) is not child&#8217;s play and one needs to learn a lot from the experts in order to make a significant contribution to the field of open source.

But again, to learn about a software and thereby contribute to its development, you need to contact the developers or contributors. This is where comes the role of Internet Relay Chat(IRC). IRC is based on a client/server architecture and facilitates chat, private messaging, file sharing and group communication in the form of channels. An IRC client is a software that can be installed on a computer and then you can connect to the server you want to. Without further ado, let us explore XChat 🙂

XChat has been written in C and is free for UNIX and Linux 🙂 but not on Windows 🙁 But still you can use XChat on Windows for 30 days for free 😀

I am going to teach you how to configure and use XChat on Ubuntu (Note : I have tested this on Ubuntu 14.04LTS).

To install XChat via command line, simply type the following command into the terminal:

<pre>sudo apt-get install xchat</pre>

Now open the XChat application from dash home.[<img class="aligncenter size-large wp-image-364" src="http://www.ktreat.com/wp-content/uploads/2015/01/11-1024x576.png" alt="1" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/11-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/11-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/11-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/11.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/11.png)

You will see a screen like this:[<img class="aligncenter size-large wp-image-366" src="http://www.ktreat.com/wp-content/uploads/2015/01/2-1024x576.png" alt="2" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/2-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/2-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/2-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/2.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/2.png)

Fill up the empty fields accordingly. Nick name is your name that will be displayed when you will be chatting on IRC. Second and third choice are there for the Nick name in case the one you choose is already in use by some other user. Also enter your desired username and the real name.

After having entered your names 😛 , you can select any network from the list below and click on connect. This will take you to their IRC directly and there you can join any channel you wish. But what if you want to join to a network that is not listed there? I am going to show you exactly how to do that 🙂

Suppose you want to join the <a title="Mozilla IRC" href="http://irc.mozilla.org" target="_blank">Mozilla IRC</a>, click on the Add button. A network by the name of New Network will come up in the list of networks. Rename it as you wish. I am going to name it Mozilla IRC.

[<img class="aligncenter size-large wp-image-369" src="http://www.ktreat.com/wp-content/uploads/2015/01/3-1024x576.png" alt="3" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/3-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/3-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/3-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/3.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/3.png)Now, we need to do some settings for this network. To proceed, click on Edit.[<img class="aligncenter size-large wp-image-371" src="http://www.ktreat.com/wp-content/uploads/2015/01/41-1024x576.png" alt="4" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/41-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/41-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/41-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/41.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/41.png)Rename the newserver/6667 entry to irc.mozilla.org(This entry should be renamed differently if you want to connect to any other server). You can tick the check box for auto connect to this network at startup if you don&#8217;t want to manually connect to the server every time you open XChat.

Now, we will need to add channels to which we want to connect automatically on startup. Again, if you don&#8217;t specify any channels here, you will have to manually join the channel every time you start XChat. To add any channel to your favorites list, click the three dots at the end of Favorite channels textbox.You will get a screen like this:[<img class="aligncenter size-large wp-image-372" src="http://www.ktreat.com/wp-content/uploads/2015/01/5-1024x576.png" alt="5" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/5-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/5-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/5-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/5.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/5.png)Click on Add to add a channel to your favorites list. You can set a password also if you want. Remember that mostly channel names start with a #, so write the name of the channel like #<name\_of\_channel>. Here, I joined #introduction. Add as many channels as you wish to join at the application startup. Click OK. Set the character set to system default. You can learn more about the remaining fields by hovering your cursor over the respective text boxes. I did not need to use them so I left them empty.[<img class="aligncenter size-large wp-image-373" src="http://www.ktreat.com/wp-content/uploads/2015/01/6-1024x576.png" alt="6" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/6-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/6-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/6-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/6.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/6.png)
  
Click Close. Select Mozilla IRC and click Connect.
  
**Note** : If you are behind a proxy server, you can go to Settings -> Preferences -> Network -> Network Setup. You can customize XChat according to your preferences no end. I am leaving it to the readers to experiment with the different settings 🙂
  
On getting connected, you will be presented with the following window. You can do any of the 3 things listed but I am just letting it go because I know that the channel I wished to join (#introduction) will be joined automatically (remember we did the setting for that just a few seconds before 😉 ). I am also going to uncheck the &#8220;Always show this dialog after connecting&#8221; thing as I don&#8217;t want it to pester me every time I connect to the server.
  
[<img class="aligncenter size-large wp-image-374" src="http://www.ktreat.com/wp-content/uploads/2015/01/7-1024x576.png" alt="7" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/7-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/7-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/7-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/7.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/7.png)See that I have joined #introduction at irc.mozilla.org successfully 🙂 Below is my username with a text box in which I can type any question I want to ask, help someone else by giving answer to his/her query and I can even type some commands from there 😎 . See this list of <a title="IRC Commands" href="http://en.wikipedia.org/wiki/List_of_Internet_Relay_Chat_commands" target="_blank">IRC commands</a>
  
[<img class="aligncenter size-large wp-image-379" src="http://www.ktreat.com/wp-content/uploads/2015/01/8-1024x576.png" alt="8" width="640" height="360" srcset="http://www.ktreat.com/wp-content/uploads/2015/01/8-1024x576.png 1024w, http://www.ktreat.com/wp-content/uploads/2015/01/8-300x169.png 300w, http://www.ktreat.com/wp-content/uploads/2015/01/8-534x300.png 534w, http://www.ktreat.com/wp-content/uploads/2015/01/8.png 1366w" sizes="(max-width: 640px) 100vw, 640px" />](http://www.ktreat.com/wp-content/uploads/2015/01/8.png)<a title="IRC Tutorial" href="http://www.irchelp.org/irchelp/irctutorial.html" target="_blank">This</a> is a good IRC tutorial.

That&#8217;s all for today. Enjoy!! And don&#8217;t forget to write your thoughts in comments below.

[subscribe2]