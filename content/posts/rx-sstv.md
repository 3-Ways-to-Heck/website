---
title: RX-SSTV
path: /blog/rx-sstv
date: '2022-11-17'
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

You’re looking at a CTF question. They give you an audio file to listen to, but after doing everything you can, whether it’s changing the file type to putting it through a spectrometer, you receive no output. What you can deduce is that it hurts your ear when you listen to it and consists of loud beeps and screeches. Most likely, you are listening to slow-scan television signals. 

Slow scan television (or SSTV for short) is a method in which images, either in monochrome or color, are transmitted through radio waves. Back then, you needed specialized equipment and was mostly used to transmit images from space. These days, SSTV is defunct as there are more efficient communication systems, but amateurs like us can now do it at home with just a PC and software. The one that I prefer to use is a free but powerful tool called [RX-SSTV.](http://users.belgacom.net/hamradio/rxsstv.htm)

There are various types of SSTV systems that will determine how the signal is translated and how much information is retained, but all of them work relatively the same. If you don’t know which mode the message is sent in, the program will either auto-detect it or just play around with various modes. In this example, we’ll use Robot 36.

Take a listen to [this](https://drive.google.com/file/d/1oQAPfjCCRYaRfCMpSRZ-qtZf9KJD6U1_/view) audio file. We can determine that the message is in SSTV due to the header. I won’t get into the specifics of how it works but it tells RX-SSTV that it is about to transmit information based on its bits. This is the first couple of distinct tones you hear in the first second of the file.

The next step is to actually get the signals to the program. There are two methods to do this: the traditional way and the modern way. Both will provide the same output. I usually use the traditional way but the modern way works just fine if you’re in a noisy environment or don’t have a microphone and speakers. The traditional way involves putting your microphone close to the speaker and letting the program listen to the audio file. If you can’t do that, however, you can link your output as an input through the use of a virtual audio cable. You can find where to get one [here.](https://vb-audio.com/Cable/) That will provide a clean, uninterrupted feed to RX-SSTV. 

I used the traditional method with the audio file I gave above. This should be your expected output, a clear image with minor distortion.