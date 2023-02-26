---
title: Cookies
path: /ctf/picoCTF/2021/cookies
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

From the name of the challenge, we can infer that we need to manipulate the website's cookies. To examine the cookies:
1. right click on the page and select `Inspect` or use the keyboard shortcut `Ctrl+Shift+I` in Chrome to open Chrome DevTools
2. click on the `Application` tab on the top bar (if you don't see it, click the `>>` to expand the options)
3. expand the `Cookies` tab under `Storage` in the left pane and click `http://mercury.picoctf.net:64944/` (or the name of the website)

You should now see a table of cookies with many columns, but really two important ones: `Name` and `Value`. Currently, we see that there is one entry: `name = -1`. Let's type a cookie name into the website's search page and see what happens (make sure to keep the `Application` tab open and observe the changes). After I typed in "snickerdoodle" (the superior cookie) into the search bar, I noticed a couple of things:
1. the value of the `name` cookie changed from `-1` to `0`
2. the page has redirected us to the endpoint `/check` (we know that because the URL is now `http://mercury.picoctf.net:64944/check`)
3. there is no flag, unfortunately, as we are presented with a message: `That is a cookie! Not very special though...`

Let's try another cookie name by clicking the `Home` button on the top right that will lead us back to the `/` endpoint with the search page.
1. If I type in `Thin Mints`, a cookie that doesn't seem to exist in their database, we see a different error: `That doesn't appear to be a valid cookie.` The value of the cookie `name` is reset back to `-1`. That wasn't very helpful.
2. If I type in `chocolate chip`, we are presented with the same `Not very special` message from before, but now the `name` cookie has a value of `1`! How exciting!

Now, we could sit here all day and try to type in cookie names, but that would be terribly inefficient. Instead, now that we have an idea of how to get the flag - to type in a cookie that the website deems as "special" - we can attempt a more programmatic approach. We already know that typing in different cookie names result in a different cookie value for `name`. Why don't we just manipulate the cookie value of `name` directly, completely bypassing the search page?

I know, it's a brilliant idea. Let's write a Python script to visit the website a bunch of times, sending a different integer as the `name` cookie value each time, until the `Not very special` message is gone.

## Solve

Here are two useful Python libraries for dealing with HTTP requests (which is essentially visiting a website):
* `urllib.request`
* `requests`

I'm going to use `urllib.request` for this challenge. You can install it with `pip install urllib`. First, we are going to need to import the module with `import urllib.request`. Next, we are going to set two constants:
* the URL
* the cookie name  

```
URL = "http://mercury.picoctf.net:64944/check"
COOKIE_NAME = "name"
```
Make sure the path has the `/check` endpoint, because we're going to need the response from that page (to check whether it contains the `Not very special` message).

Next, we're going to use a `for` loop to run through the integers from 1 to, let's say, 50 (we can always change this value later if it doesn't work). We will initiate a `Request` object with the following: `req = urllib.request.Request(URL)`. We will also add our cookie as a header (which is just some data sent along with the request) like so: `req.add_header("Cookie", COOKIE_NAME + "=" + str(COOKIE_VALUE))`. After we send the request, we will read the response as bytes and decode it: `response = urllib.request.urlopen(req).read().decode()`. Finally, we're going to use an `if` statement to check whether the response string contains the `Not very special` message. If it does not, we will print out the response (which will hopefully contain the flag) and exit the `for` loop.

Now, let's run the script in the terminal: `python3 cookies.py`.

And...we got the flag! `picoCTF{3v3ry1_l0v3s_c00k135_cc9110ba}`

## Notes

If you're on Linux, you can use pipe the output of the script to a file and use `grep` to search the file for the word "flag" or "picoCTF". Otherwise, you could just use `Ctrl+F`. If you prefer, you could make your script print out the valid `COOKIE_VALUE` and input it into the actual website yourself so you can see the rendered output instead of just the HTML code.

## Resources

You can find the full script below or [here](cookies.py) as a file.

```
import urllib.request

URL = "http://mercury.picoctf.net:64944/check"
COOKIE_NAME = "name"

for COOKIE_VALUE in range(100):
	req = urllib.request.Request(URL)
	req.add_header("Cookie", COOKIE_NAME + "=" + str(COOKIE_VALUE))
	response = urllib.request.urlopen(req).read().decode()
	if "Not very special though" not in response:
		print(response)
		break
```