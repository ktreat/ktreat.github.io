---
id: 86
title: 'Behind HTTPS: RSA Encryption &#8211; The Basics'
date: 2014-08-01T17:06:33+00:00
author: tapananand

guid: http://www.ktreat.com/?p=86
permalink: /behind-https-rsa-encryption-the-basics/
custom_total_hits:
  - "000001967"
categories:
  - Encryption
  - Internet Security
---
All of us use websites like facebook, google, and online payment/transaction websites like irctc, paytm, godaddy, and uncountably many. What you must have also noticed in these websites is that when you open them they use https protocol instead of http, which is used by most others. And by the way if you don&#8217;t know **these people paid to get https** 😛 . So why **&#8220;waste&#8221;** the money?? Well let me tell you something brother 😛 they are **&#8220;wasting&#8221;**  their money to save yours or to save your passwords and your personal information. How? you say. Read on to find out&#8230;
  
When you use a http website, any form data you send is sent unencrypted and hence a **hacker** can read your passwords, credit card number etc by **sniffing 🙁 .** I&#8217;ll probably have a post on how to do this in various ways in the future 🙂 . So if a site asks for very sensitive information and it is not https you may be at risk.

> **NOTE:** Some sites are not https by default but instead only some sensitive pages are https.

So, how does HTTPS prevent this?? It does this by using an encryption algorithm under the **[SSL(Secure Socket Layer) Protocol](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)**. The encryption algorithm used by **SSL** is **RSA**, the topic of our discussion. But before we talk about **RSA** more let&#8217;s know a bit more about encryption to understand the importance of RSA. All encryption algorithms employ some techniques to scramble the message in a way that it can only be retained with the help of a string called as **the Key**. The scrambled message is called **cipher**. So, things look like this in encryption:
  
<!--more-->

<pre>M = Message

K = Key

C = Cipher

E = Encryption algorithm

D = Decryption Algorithm

<span style="text-decoration: underline;"><strong>At Sender:</strong></span>

    C = E(M, K)

Send C to Receiver.

<span style="text-decoration: underline;"><strong>At Receiver:</strong></span>

    M = D(C, K)
</pre>

Encryption is of two type based on this key:

  1. <span style="text-decoration: underline;"><strong>Symmetric Encryption: </strong></span>The same key is used on both sides i.e. Encryption and Decryption. So, the above illustration is for symmetric encryption. **e.g.: AES, IDEA, etc.**
  2. <span style="text-decoration: underline;"><strong>Asymmetric Encryption</strong>:</span> Different keys for encryption and decryption. **e.g. RSA.**

So, in symmetric encryption a random key is generated at sender, the message is encrypted and both key and cipher is sent to the receiver. Now, this is where the problem occurs, If the hacker knows the encryption algorithm in use or somehow guesses it, he can get the key when being sent and decrypt the message. So, we come back where we started &#8211; we need to encrypt the key now 😐 . This is where RSA or asymmetric algorithms come to aid. And we&#8217;ll explore the RSA algorithm now to understand how. By the way, RSA was first published in 1977 by Ron <span style="text-decoration: underline;"><strong>R</strong></span>ivest, Adi <span style="text-decoration: underline;"><strong>S</strong></span>hamir and Leonard <span style="text-decoration: underline;"><strong>A</strong></span>dleman.

So, RSA uses a pair of keys instead of one &#8211; **a public key** for encrpytion and **a private key** for decryption. Since the public key doesn&#8217;t decrypt the message so we can share it without any problems. However, one must note that both private and public keys are generated using the same algorithm and a hacker can theoretically derive the private key from the public key but, the way these keys are generated, practically it will require his many future generations to do nothing else but this 😛 . Though Quantum Computing shows that it can be done quickly, matter for another time though 🙂 .

So how does RSA achieve this? Well, I&#8217;ll post a bit detailed algorithm in a future post but here I will tell the basics.

What RSA does is pick two very large prime numbers.  Large to the extent that they are of order 2^1024. It then multiplies these two numbers. Now u get a huuuuuge number, which has only two factors. This number is used to generate the public and private keys. Now, if you think about it, multiplying two large numbers is **relatively easier** than factoring a number into its only two factors. And thus you have now created a problem that is very hard for the computer and hence, not solvable practically in time. So here is an illustration for RSA:

<pre>Receiver Generates two keys:

PuK = Public Key

PrK = Private Key

Sender asks for receiver's public key.

<span style="text-decoration: underline;"><strong>At Sender:</strong></span>

C = E(M, PuK)

Send C to Receiver.

<span style="text-decoration: underline;"><strong>At Receiver:</strong></span>

M = D(C, PrK)</pre>

So, that&#8217;s all for today. You can read the RSA algorithm in a bit detail in [this post](http://www.ktreat.com/?p=148). If you have any comments, suggestions, etc please <span style="text-decoration: underline;"><strong><a href="http://www.ktreat.com/?p=86#respond">comment</a></strong></span> By the way, you can subscribe to the newsletter to my blog and receive instant updates to your email whenever there is a new post. Here is the form below if you haven&#8217;t subscribed yet.

[subscribe2]