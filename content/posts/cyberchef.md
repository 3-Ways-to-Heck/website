---
title: CyberChef
path: /blog/cyberchef
date: '2023-01-06'
type: post
authors:
  - jack-keifer
draft: false
hero:
  image: ../images/dummy.jpg
  large: false
  overlay: true
tags:
  - beginners
---

[CyberChef](https://gchq.github.io/CyberChef/) is one of those cybersecurity tools that you can never forget about. Think of it as the Swiss Army Knife for all conversions. It can encode and decode various ciphers, translate obscure bases, and a whole lot of other miscellaneous uses. Not only is it simple and easy-to-use but you can also stack many operations on top of each other. For example, if a message is encrypted multiple times, such as octal and then binary, you can do that in one action by clicking one action after the other. 


![image](https://user-images.githubusercontent.com/71365470/112068962-2de70680-8b28-11eb-979e-ce7defcd9b37.png)

Let’s try something you’ll find in a CTF. I will be using CyberChef to brute force a XOR encryption. If you haven’t read up on XOR yet, you can check out my article on the topic. This is the exact same problem that we went over except I am given no key. We’re given this [text](https://drive.google.com/file/d/1WI_LSwn9otxBCo-jTv-r6nc-6jM0PiZJ/view) (it could be invisible to you):

![image](https://user-images.githubusercontent.com/71365470/112069082-671f7680-8b28-11eb-9548-79a5f0f21963.png)

While it may not look like anything, and all we see are symbols we can’t recognize, this ciphertext is very important. Double click and copy the ciphertext. Let’s go to the CyberChef website and select the XOR tool. Paste the ciphertext into the input. Most CTFs have a wrapper for their flag that’s usually stated in their rules. I’ll make one up, so in this case, let’s put the string “flag” as the known-plaintext under the recipe section.

![image](https://user-images.githubusercontent.com/71365470/112069150-8d451680-8b28-11eb-894d-06932279833b.png)

Now we have to figure out the key length. We know that the key cannot be larger than the number of characters in the ciphertext, and we know that it’ll take the computer longer brute force every combination that has a longer key. Let’s start from the bottom at a key length of 1, and hit the bake symbol on the bottom. If you check the output, there’s nothing. Try 2 instead. If you don’t see results immediately, feel free to give the program some time; it has to go through a lot. Bingo, we see 4 flags with relatively the same information.

![image](https://user-images.githubusercontent.com/71365470/112069208-a8b02180-8b28-11eb-8e69-2ff1986bb1ea.png)

As you can see, they are all a variation of flagdogs. Usually, CTFs will either tell you if the flag is case-sensitive or not and if it will allow multiple attempts. If we want to figure out the key, we can just compare the numbers to an [ASCII chart](https://upload.wikimedia.org/wikipedia/commons/c/cf/USASCII_code_chart.png). The keys are all different cases of “hi” which is the exact same key we went over in the XOR tutorial.