# Web Exploitation

## Cookies

Flag : `picoCTF{3v3ry1_l0v3s_c00k135_88acab36}`
<br>
The challenge page gives a URL to a dummy page with a text box to enter cookie names.
![image](/content/pico_webexp_cookies_1.png)
I entered `peanut butter` as my first guess and it showed : 
![image](/content/pico_webexp_cookies_2.png)
As it said `Not very special though...`, the goal is clearly to get some correct value for the cookie,
which will in return the flag.
To monitor what the value of the cookie meant I looked at `Inspect Element`.
![image](/content/pico_webexp_cookies_3.png)
As I made other guesses, I noticed the value change. 
In an attempt to reverse engineer this I entered an integer value in the element and refreshed. 
This gave another cookie name. I entered all numbers starting from 1 until i reached 18...
![image](/content/pico_webexp_cookies_4.png)

Learnt :
- Inspecting Cookie elements
- Manipulation in cookie handling

Incorrect methods I tried :
- Guessing all cookie names (naturally it failed)
- Tried changing all the other parameters except the main value

## SOAP

