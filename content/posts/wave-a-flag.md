---
title: Wave a Flag
path: /ctf/picoCTF/2021/wave-a-flag
date: '2021-04-30'
type: post
authors:
  - ethan-evans
draft: false
hero:
  image: ../images/dummy.jpg
  large: false
  overlay: true
tags:
  - picoctf
---

![image](https://user-images.githubusercontent.com/71365470/112552515-3174ca80-8d80-11eb-95e2-347426f611a8.png)

## Think

Here we are given one file, `warm`, an ELF executable. This means If you are using windows, you will need to either get this file onto a *nix system/VM or use the provided webshell using `wget`, `curl`, or the like.

Running the file prints a message saying to pass the argument `-h`. And there we have the flag.

```shell
> ./warm 
Hello user! Pass me a -h to learn what I can do!

> ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_6635aa47}
```

## Solve
```picoCTF{b1scu1ts_4nd_gr4vy_6635aa47}```

## Resources
- TBA