---
title: Who are you?
path: /ctf/picoCTF/2021/who-are-you
date: '2021-04-30'
type: post
authors:
  - katrina-lee
draft: false
hero:
  image: ../images/dummy.jpg
  large: false
  overlay: true
tags:
  - picoctf
  - web-exploitation
---

## Think

When we visit the website, we are greeted with a message: `Only people who use the official PicoBrowser are allowed on this site!`. Seeing the word "browser" in the context of a restricted website makes me immediately think of User-Agents. When we visit a website, the client sends some information to the server, including our browser, operating system, and device information. So, let's:
1. right click on the page and select `Inspect` or use the keyboard shortcut `Ctrl+Shift+I` in Chrome to open Chrome DevTools
2. click on the 3 vertical dots (&#8942;) on the top bar >> More tools >> Network conditions

A new `Network conditions` tab will pop up on the bottom pane.
1. Uncheck the `Select automatically` box
2. Select `Custom...` from the dropdown menu
3. Type `PicoBrowser` into the "User agent" box
4. Reload the page to active the changes

Unfortunately, we don't have the flag yet. Now, there's a message saying `I don't trust users visiting from another site.`. Logically, it's probably another header thing. Let's do some research on how websites know where you came from. It seems like there's a header called the `Referer`. At this point, I'm pretty sure there will be more headers, so let's just write a quick python script to make one request to the page with the correct headers and print the response.

## Solve

First, we need to import the `requests` module: `import requests`. Then, let's set our `URL` variable and initialize a dictionary of headers.
```
URL = "http://mercury.picoctf.net:34588/"
headers = {"User-Agent": "PicoBrowser"}
```
Since the message condemns "visiting from another site," we want to set the `Referer` equal to the same site. Add a key-value pair to the `headers` dict accordingly: `"Referer": URL`.

Now, we need to actually make the HTTP GET request:
```
r = requests.get(URL, headers=headers)
print(r.text)
```

When we run our script, we get another error message: `Sorry, this site only worked in 2018.` This one seems pretty obvious; we just need to change the date header: `"Date": "2018"`.

Next message: `I don't trust users who can be tracked.` A quick google search later, and we have another key-value pair: `"DNT": "1"`.

Now, we have: `This website is only for people from Sweden.` The `X-Forwarded-For` header informs the website of the client's IP address. So, just find a Sweden IP address on google. Here's mine: `"X-Forwarded-For": "188.150.107.218"`.

Then, `You're in Sweden but you don't speak Swedish?` Search up the Swedish (Sweden, not Finland) ISO language code: `"Accept-Language": "sv-SE"`.

And...we got the flag! `picoCTF{http_h34d3rs_v3ry_c0Ol_much_w0w_79e451a7}`

## Notes

Quick note on how to view HTTP responses in a nice and pretty format: there are really two main ways.
1. Write the output into a file named with a `.html` extension (either by copying & pasting or with Python) and open it in your browser.

    With Python:
    ```
    with open("response.html", "w") as f:
        f.write(r.text)
    ```

2. Look at it in your terminal and use Python's `.split()` function or RegEx to extract only the error message text.

    With `.split()`:
    ```
    msg = r.text.split('<h3 style="color:red">')[1].split("</h3>")[0]
    ```

    With RegEx:
    ```
    import re
    pattern = re.compile('<h3 style="color:red">(.*)</h3>')
    msg = pattern.search(r.text)
    print(msg.group(1))
    ```

## Resources

* [HTTP headers - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/)

You can find the full script below or [here](who_are_you.py) as a file.

```
import requests

URL = "http://mercury.picoctf.net:34588/"
headers = {"User-Agent": "PicoBrowser", "Referer": URL, "Date": "2018", "DNT": "1", "X-Forwarded-For": "188.150.107.218", "Accept-Language": "sv-SE"}

r = requests.get(URL, headers=headers)
print(r.text)
```