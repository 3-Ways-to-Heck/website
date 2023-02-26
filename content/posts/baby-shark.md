---
title: Wireshark doo dooo do doo
path: /ctf/picoCTF/2021/baby-shark
date: '2021-05-27'
type: post
authors:
  - nathan-wagner
draft: false
hero:
  image: ../images/dummy.jpg
  large: false
  overlay: true
tags:
  - picoctf
  - packet-tracer
---
![image](https://user-images.githubusercontent.com/71365470/112552515-3174ca80-8d80-11eb-95e2-347426f611a8.png)

## Think

When opening up the file you see a lot of connections to wsman subscriptions. However, if you continue to scroll down there is a GET request at packet 823, the GET is asking for a text file. Going into file -> export objects -> HTTP to find the text file we can see 2 files that standout: one being text/plain and the other being text/html. The text/plain opens to a single word: none. The other file, text/html, shows an encrypted file that contains:

```picoCTF{22e018bb8282e9d7852ed4e65f70a26524dabef78cf41e1db45c070c94621c57}```

Decoding this with base64 gives us:


## Solve
```picoCTF{p33kab00_1_s33_u_deadbeef}```

## Resources
- TBA
