---
id: 302
title: Getting Ubuntu Partitions to show on Windows
date: 2015-01-09T14:44:56+00:00
author: tapananand

guid: http://www.ktreat.com/?p=302
permalink: /getting-ubuntu-partitions-to-show-on-windows/
custom_total_hits:
  - "000002378"
  - "000002378"
categories:
  - Linux
  - Ubuntu
  - Windows
---
I am among the many people who have a dual boot of Ubuntu and Windows 7 on their machine. Many times when I am investigating the internals of a program by looking into its assembly and other Linux Stuff, I&#8217;ve to switch to Ubuntu. But also being a web developer I like to work on Dreamweaver for my web projects. Though Ubuntu also has some good web editors like Geany, but I really love Dreamweaver for my projects. This forces me to switch back to windows.

Now, when I am using Ubuntu I can easily access Windows partitions and thus access any files I want. But when I am on Windows, I can&#8217;t access Ubuntu partitions. This post describes why this happens and then gives two solutions. So let&#8217;s get started.

When we install Ubuntu, it basically requires 4 partitions. The following table shows these partitions (assuming an install in 60GB):

<table style="width: 90%; margin: 0px auto 10px auto; text-align: center;">
  <tr style="background-color: #5cb85c; color: #fff;">
    <th style="text-align: center;">
      Filesystem Type
    </th>
    
    <th style="text-align: center;">
      Mount Point
    </th>
    
    <th style="text-align: center;">
      Recommended Size
    </th>
  </tr>
  
  <tr>
    <td>
      ext4/ext3
    </td>
    
    <td>
      / (the root filesystem)
    </td>
    
    <td>
      10GB
    </td>
  </tr>
  
  <tr>
    <td>
      ext4/ext3
    </td>
    
    <td>
      /boot (optional)
    </td>
    
    <td>
      500MB
    </td>
  </tr>
  
  <tr>
    <td>
      swap (optional)
    </td>
    
    <td>
      None
    </td>
    
    <td>
      512MB (twice the size of your RAM to enable hibernation)
    </td>
  </tr>
  
  <tr>
    <td>
      ext4/ext3
    </td>
    
    <td>
      /home
    </td>
    
    <td>
      The Remaining Space (~50GB)
    </td>
  </tr>
</table>

You can <a title="Install Ubuntu with manual partitioning" href="http://askubuntu.com/a/343352/160769" target="_blank">manually choose for yourself to create these partitions</a> when installing Ubuntu or <a title="Installing Ubuntu 14.04 LTS Alongside Windows" href="http://www.ktreat.com/installing-ubuntu-14-04-lts-alongside-windows/" target="_blank">let Ubuntu create them for you</a>.

** /boot** and **swap** above are optional but recommended. **/** and **/home** are required and are the most important ones. So, now we know enough to explore the reason for Windows not showing the Ubuntu Partitions. We see that the root partition of Ubuntu is of type ext4 or ext3. Windows only understands <a title="NTFS" href="https://en.wikipedia.org/wiki/NTFS" target="_blank">NTFS</a> and <a title="File Allocation Table" href="https://en.wikipedia.org/wiki/File_Allocation_Table" target="_blank">FAT</a> filesystems. Thus, windows can&#8217;t show these partitions in the explorer.

So, now we know the reason, but how to fix this? Let us see two possible solutions:

### An extra NTFS partition in Ubuntu

We know that Ubuntu can access Windows partitions (as it could access windows partitions which are NTFS), so why don&#8217;t we exploit this? 💡 This is what this solution does. But this solution requires you to install Ubuntu by choosing the manual partition option. What we do is we create an extra partition when creating other partitions for Ubuntu. We format this file system as an NTFS partition and thus both Windows and Ubuntu can access it. You can also reduce the size of your **/home** partition in this case. Use this new partition for storing your other files.

But what if you have already installed Ubuntu or don&#8217;t like this solution? Well, Solution 2 is just for you.

### Using a Software on Windows &#8211; ext2fsd

Well, there is a Software for this as well and it is awesome 🙂 . This software shows you **/ (root)** partition along with your other Windows partitions with a drive letter. The software is called ext2fsd and you can download it <a title="Ext2fsd" href="http://sourceforge.net/projects/ext2fsd/files/" target="_blank">here</a>. After you install this, you may be asked to choose a drive letter for the Ubuntu Partition. Also you need to check if it is set to start automatically on boot. You can check this in **Tools -> Service Management.** It usually is started by itself though. This section also has the option (checkbox) whether to mark the partitions to be mounted in read-only mode.

There is one minor issue with this method though. When you mount the partitions in read-only mode everything is OK. But, if you want to write to it you have to un-tick the check box mentioned above. This setting can be a bit tricky though. It is not highly recommended to write using **ext2fsd** to an Ubuntu partition. I have been using this software from a long time and don&#8217;t require much to write to it, but when I do, I write without hesitation as I have a regular backup of my files. So, I recommend you to do so as well before writing. I have had a problem after writing to the partition once. I could not boot into Ubuntu for some time. After several reboots I was in finally 🙂 .

So, that&#8217;s all I had. Hope you liked it. Comment if you have any. Subscribe for email updates below:

[subscribe2]