# Miscellaneous

## freakada 3301

The challenge is to decode or search the give image for the flag.

![image](/content/nitectf_misc_freakada_1.png)

After reading the text in image and analysing it, 
I couldn't come across any useful hints.
So I turned towards common steganography tools, here `exiftool`.

![image](/content/nitectf_misc_freakada_2.png)

Clearly the only unusual information here is the subject field.

```
ZIT HQZI OL GWLEXKTR, WXZ ZIT ZKXZI SOTL OF ZIT LIQRGVL. LTTA ZIT HQZZTKFL. QDGFU ZIT EIQGL, Q WTQEGF QVQOZL: izzhl://woz.sn/yktqatlztof0. GFSN ZIT VGKZIN VOSS LTT ZIT XFLTTF. ZIT PGXKFTN IQL PXLZ WTUXF
```

Assuming it to be some sort of cipher, I put it into a Vignere decoder first and then a Caeser decoder.
Neither worked so i tried a mono-alphabetic substitution decoder and it worked.

```
THE PATH IS OBSCURED, BUT THE TRUTH LIES IN THE SHADOWS. SEEK THE PATTERNS. AMONG THE CHAOS, A BEACON AWAITS: HTTPS://BIT.LY/FREAKESTEIN0. ONLY THE WORTHY WILL SEE THE UNSEEN. THE JOURNEY HAS JUST BEGUN
```

The embedded link `HTTPS://BIT.LY/FREAKESTEIN0.` led to a proton drive with an image file `ducky.png`.

![image](/content/nitectf_misc_freakada_3.png)

Again using `exiftool` was futile and didnt yield anything so i tried used `binwalk`.
This led me to a zip file `_ducky.jpg.extractor`, extracting which got me a text file `sexret.txt`.
Catting this file returned a github repo link `https://github.com/freakada-3301`.
<br>
(The next part took hours and a lot of help) 
Looking through the past commits and included readme and whispers of the forgotten files, 
I got a link to a discord server.
(I can't include more info because i forgot how i pieced together all the clues while writing the writeup)
<br>
The discord server had a bot called `freakada` which asked me to multiply three prime numbers.
I tried an initial 3301 cuz duh...and then it asked for `3301*x*y`.
The missing values were obtained from the original exiftool results giving the image size `449*503`.
<br>
The bot then returned a set of co-ordinates to `Freaky Backshots Cliffs`.
(inside joke its a place on the MIT campus)
The reviews of the place had a QR code which upon scanning returned an audio file.
<br>
Having no idea what to do with an audio file I looked up how to convert it to a spectogram.
This led to me using the `ffmpeg` tool.

![image](/content/nitectf_misc_freakada_4.png)

The returned spectogram :

![image](/content/nitectf_misc_freakada_5.png)

This gave us the first part of the flag `nite{4_wannabe_`
<br>
Further decoding the suspicious morse code in the image, i got the key `freekey` to the earlier cipher i obtained 
through the github repo, which returned the second half of the flag `1nt3rn3t_my5tery}`
