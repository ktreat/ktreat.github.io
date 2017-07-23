---
id: 178
title: 'Android L &#8211; the cool new Android'
date: 2014-08-28T17:13:21+00:00
author: tapananand

guid: http://www.ktreat.com/?p=178
permalink: /android-l-the-cool-new-android/
custom_total_hits:
  - "000001434"
categories:
  - Android
  - Google
  - Misc
---
Just like every year, Google I/O was held in June this year and a lot of new technologies and upgrades on the existing ones were announced. So, this is a multi-part series in which I&#8217;ll introduce you to these new technologies and upgrades. I&#8217;m writing this series because I&#8217;m really enthusiastic about Google&#8217;s technologies and would like to share them with all of you.

So, let&#8217;s start with the big 0ne 🙂 i.e &#8220;**the biggest release in the history of Android&#8221;** &#8211; as said by one of the Directors of Engineering of Android &#8211; Dave Burke. It&#8217;s called Android L &#8211; Yes!! no mouthwatering name this time just **&#8220;L&#8221;** 😛 .

It has over 5000 new APIs and a **&#8220;fresh, bold and new look&#8221;**.

### The All new look

The project was based on a new way of thinking called **material design.** The L UI will be displayed as if it&#8217;s on an intelligent material that can change shape in response to touch. The whole UI turns 3 D. Developers can specify an elevation value for any UI surface and the framework will render it perfectly in 3D with virtual light sources. See the video below:

<center>
</center>Also a new library is added called Palette using which the developers can extract and use colors from images to make your app look better. There is a ripple effect when touching the elements like a button in the UI. Also the system font Roboto was updated to be usable on all screens even watches. The developers can now even customize the animations when entering and exiting an activity even between apps. Read all about its design features 

<a title="Google Design" href="http://www.google.com/design/" target="_blank">here</a>. See how the Gmail app looks in the new material design concept:

[<img class="aligncenter wp-image-279 size-large" src="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.19.58_2014.08.28_21.16.26-1024x576.jpg" alt="" width="640" height="360" srcset="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.19.58_2014.08.28_21.16.26-1024x576.jpg 1024w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.19.58_2014.08.28_21.16.26-300x169.jpg 300w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.19.58_2014.08.28_21.16.26-533x300.jpg 533w" sizes="(max-width: 640px) 100vw, 640px" />](/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.19.58_2014.08.28_21.16.26.jpg)

Let&#8217;s concentrate on its many other features:

  1. ### Enhanced Notifications
    
    Now, you can access your notifications right from the lock screen itself without having to pattern unlock it and all 🙂 .[<img class="aligncenter wp-image-280 size-large" src="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.25.44_2014.08.28_21.19.37-1024x576.jpg" alt="" width="640" height="360" srcset="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.25.44_2014.08.28_21.19.37-1024x576.jpg 1024w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.25.44_2014.08.28_21.19.37-300x169.jpg 300w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.25.44_2014.08.28_21.19.37-533x300.jpg 533w" sizes="(max-width: 640px) 100vw, 640px" />](/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.25.44_2014.08.28_21.19.37.jpg)
  
    Android will organize and prioritize your notifications by analyzing your behavior so that only the most relevant notifications show up on the lock screen. You can double tap a notification to open the corresponding app or swipe it away to dismiss. Swipe upwards to unlock the screen.</li> 
    
      * ### Heads up notification
        
        Suppose you are playing a game and your are about to get your high score when somebody calls 😛 irritating isn&#8217;t it. Well Heads up notification solves this problem. You are shown the caller info. at the top without interrupting the game and you can then decide to answer or reject. See below:[<img class="aligncenter wp-image-281 size-large" src="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.26.46_2014.08.28_21.26.19-1024x576.jpg" alt="" width="640" height="360" srcset="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.26.46_2014.08.28_21.26.19-1024x576.jpg 1024w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.26.46_2014.08.28_21.26.19-300x169.jpg 300w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.26.46_2014.08.28_21.26.19-533x300.jpg 533w" sizes="(max-width: 640px) 100vw, 640px" />](/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.26.46_2014.08.28_21.26.19.jpg)</li> 
        
          * ### Personal Unlocking
            
            Under this feature your android device can determine if it&#8217;s in a trusted environment or not using the locations you can designate, signals from your Bluetooth watch, etc. If it detects a trusted environment it will not show the tedious pattern/pin lock and will just show the swipe unlock. Handy 🙂 .</li> 
            
              * ### Material Design for web
                
                The web designers can also design their websites with the look and feel of material design you see above using a powerful UI library called <a title="Polymer" href="http://www.polymer-project.org/" target="_blank">Polymer</a>. It also supports animations at 60 frames per second.</li> 
                
                  * ### Redesigned Recents to multitask
                    
                    Currently the recents show only the recent apps but Android L provides a new API to allow apps to populate multiple items in recents. It was demonstrated by Avni Shah , Director of product management chrome, using chrome as an example. They showed all the chrome tabs being populated in the recents, handy isn&#8217;t it? 🙂[<img class="aligncenter wp-image-282 size-large" src="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.33.07_2014.08.28_22.04.29-1024x576.jpg" alt="" width="640" height="360" srcset="/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.33.07_2014.08.28_22.04.29-1024x576.jpg 1024w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.33.07_2014.08.28_22.04.29-300x169.jpg 300w, /wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.33.07_2014.08.28_22.04.29-533x300.jpg 533w" sizes="(max-width: 640px) 100vw, 640px" />](/wp-content/uploads/2015/01/Google-I_O-2014-Keynote-YouTube.mp4_snapshot_00.33.07_2014.08.28_22.04.29.jpg)</li> 
                    
                      * ### App indexing
                        
                        App indexing is a feature that  allows developers to connect pages from their website with specific content within your smartphone app. This enables smartphone users who have your app installed to open it directly from relevant mobile search results on Google. This was earlier open to only a few apps but now it has been opened to all apps. There is an API to allow developers to show suggestions for content that the user has already seen in the app while searching for the same thing on Google.</li> 
                        
                          * ### Performance in L
                            
                            Google has completely changed the Android Virtual machine. There is a new one call **ART** now which is replacing the earlier one which was <a title="Dalvik" href="http://en.wikipedia.org/wiki/Dalvik_%28software%29" target="_blank"><strong>Dalvik</strong></a>. The new VM ART is more memory efficient now with the introduction of a new garbage collector which applies a slower but intensive moving collection on background apps. Some features of ART:
                            
                            <ul type="square">
                              <li>
                                Fully 64-bit compatible.
                              </li>
                              <li>
                                Larger number of registers.
                              </li>
                              <li>
                                Newer Instructions.
                              </li>
                              <li>
                                Cross Platform support.
                              </li>
                            </ul>
                            
                            There is introduction of Bluetooth 4.1 into L. Also project volta that gives you an improved interpretation of battery data that allows you to save your battery better.</li> 
                            
                              * ### Factory Reset Protection
                                
                                If your phone is stolen users can disable their phone through Google Play Services.</li> </ol> 
                                
                                So, that was all for Android L and this part of the I/O series. Will post more in the future &#8211; about Android in your watch, in your TV, and in your Car. Thanks for reading. Comment if you have any.
                                
                                [subscribe2]