---
title: Python Wrangling
path: /ctf/picoCTF/2021/python-wrangling
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

![image](https://user-images.githubusercontent.com/71365470/112552435-0c805780-8d80-11eb-98d7-583f97c3e5c6.png)

## Think

Here we are given three files. A `ende.py`, `pw.txt`, and `flag.txt.en`.

Runnning `python ende.py -h` gives us a list of arguments. In our case we want to decrypt `flag.txt.en` using `-d`. It prompts to enter a password, so you just pass the contents of `pw.txt`.

```shell
> python ende.py -d flag.txt.en
Please enter the password: 68f88f9368f88f9368f88f9368f88f93
```

## Solve

And we get the final flag: ```picoCTF{4p0110_1n_7h3_h0us3_68f88f93}```