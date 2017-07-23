---
id: 148
title: 'Behind HTTPS: RSA Encryption &#8211; The Algorithm'
date: 2014-08-05T17:06:06+00:00
author: tapananand

guid: http://www.ktreat.com/?p=148
permalink: /behind-https-rsa-encryption-the-algorithm/
custom_total_hits:
  - "000002786"
categories:
  - Encryption
  - Internet Security
---
This post is a sequel to the previous post on this topic: [Behind HTTPS: RSA Encryption – The Basics](http://www.ktreat.com/?p=86). I hope you remember the basics mentioned in that post. You may want to revisit it, if you like. In this post, however, we will discuss the algorithm used by RSA in a bit detail. So lets get started.

Here is the  illustration of RSA from the previous post:

<pre>Receiver Generates two keys:

PuK = Public Key

PrK = Private Key

Sender asks for receiver's public key.

<span style="text-decoration: underline;"><strong>At Sender:</strong></span>

C = E(M, PuK)

Send C to Receiver.

<span style="text-decoration: underline;"><strong>At Receiver:</strong></span>

M = D(C, PrK)</pre>

We will discuss the RSA algorithm in three different parts:

  1. [Generating the key pair(public and private key).](#gen)
  2. [Encryption.](#enc)
  3. [Decryption.](#dec)

<a name="gen"></a>

### Generating the Key Pair:

Generate two big prime numbers, p and q, pseudo randomly. These numbers are of the order of magnitude of 2^1024 in practice but we&#8217;ll choose **p = 23 and q = 43,** just to be able to demonstrate here otherwise this post would be filled with big numbers only 😛 .

Now,

<pre>n = p * q = 23 * 43 = 989.
m = (p - 1) * (q - 1) = 22 * 42 = 924.
</pre>

Now, find a number **e** that is coprime with m and less than m, i. e.:

<pre>find e such that gcd(e, m) = 1</pre>

Generally, in practice we pick **e = 65537,** which is a prime by itself, if it&#8217;s coprime with m. But, here we&#8217;ll pick **e = 5**(You can see that **gcd(5, 924) = 1**).

Now, we are going to pick one final number 🙂 and it&#8217;s called **d** and we pick d such that:

<pre>de = 1(mod m)</pre>

i.e. we pick d such that **d multiplied by e gives remainder 1 when divided by m.** This is a simple problem of modular arithmetic(for those interested).

So, we pick **d = 185:**

<pre>185 * 5 = 925
925 % 924 = 1</pre>

So, we have got 4 numbers:

<pre>e = 5
n = 989
m = 924
d = 185
</pre>

So, the keys are:

<pre>Public Key = PuK = (e, n) = (5, 989)
Private Key = PrK = (d, n) = (185, 989)
</pre>

So, our prime numbers don&#8217;t appear anywhere and it is very difficult and expensive for the computer to try and find out p and q and thus find d and m, in practice(**Remember p and q are very large in practice and so is n &#8211; so factoring them will take ages 😛** ).
  
<a name="enc"></a>

### Encryption:

During Encryption,the receiver generates the key pair and the sender asks for it and sends the encrypted message. The sender breaks the message into chunks and then encrypts it. So, lets try and encrypt **&#8220;KTREAT&#8221;**, we&#8217;ll use ASCII values as the values of the characters:

<pre>For each character m, the cipher <strong>C = power(m, e) mod n
</strong>K = 75, C1 = 75 ^ 5(mod 989) = <strong>715</strong>
T = 84, C2 = 84 ^ 5(mod 989) = <strong>398</strong>
R = 82, C3 = 82 ^ 5(mod 989) = <strong>395</strong>
E = 69, C4 = 69 ^ 5(mod 989) = <strong>46</strong>
A = 65, C5 = 65 ^ 5(mod 989) = <strong>770</strong>
T = 84, C6 = 84 ^ 5(mod 989) = <strong>398</strong>
</pre>

These ciphers C1 through C6 are what is sent to the receiver.
  
<a name="dec"></a>

### Decryption

So, having received the ciphers sent from the sender, the receiver decrypts them using the private key(which was not made public) as follows(the calculations below were performed using a C program, by the way, so don&#8217;t ask me what calculator I used 😛 . You can also calculate these using a very good tool called Microsoft Math, really awesome.):

<pre>For each cipher C, message <strong>m = power(c, d) mod n</strong>
C1 = 715, m1 = 715 ^ 185(mod n) = 75 = <strong>K</strong>
C2 = 398, m2 = 398 ^ 185(mod n) = 84 = <strong>T</strong>
C3 = 395, m3 = 395 ^ 185(mod n) = 82 = <strong>R</strong>
C4 =  46, m4 =  46 ^ 185(mod n) = 69 = <strong>E</strong>
C5 = 770, m1 = 770 ^ 185(mod n) = 65 = <strong>A</strong>
C6 = 398, m1 = 398 ^ 185(mod n) = 84 = <strong>T
</strong></pre>

So, there you go, we&#8217;ve got our original message &#8211; **KTREAT **back. And that&#8217;s all for today and RSA algorithm. Thanks for reading, hope you liked it. Comment if you have any.

[subscribe2]