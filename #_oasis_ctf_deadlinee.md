# OASIS 
## Welcome
The first challenge was the easiest, the flag was provided to us in the description. 
```OASIS{h411!d4y_says_w41c0m3_t0_7h3_04515}```
## Flagged
The second challenge required us to go through the discord server and find the flag hidden somewhere on the server.
Found the flag in the description
```OASIS{0H_SN4P_Y0U_F0UND_M3_1N_7H3_D3SCR1P710N}```
## I swear it was right here
This challenge asked us to find the flag on the cryptonite instagram page.
Finding the flag was easy enough all we had to do was find the oasis post and the flag was in the caption.
```OASIS{easy_osinsta}```
## Ready Player One?
Upon playing the audio file we realised that the audio was in morse code. Using a morse code translater we got M0R5EM4N1PU7470R.
We converted the text into the flag format.
```OASIS{M0R5E_M4N1PU7470R}```
## Arte-Miss?
The attechment in this challenge was an image file.
Dowloaded the image onto my laptop so i could search for ```OASIS``` as we knew that flags started with OASIS.
We tried doing this with the grep command initally but that didnt help us out much.
We then looked for alternate codes we could run to find the information.
``` strings mirage.jpg | grep "OASIS" ```
Finally we found the flag
```OASIS{m4ta_af_04515}```
## String me to sleep
The attchement in this challenge is a text file which is probably the entire ready player one novel.
Simply used grep and searched for ```OASIS{``` and found the flag.
```grep OASIS{ library.txt```
And thus the flag
```OASIS{y0u_fou7d_m3}```
##This or that?
Spend very long on this challenge and could not figure out how to go further after converting hexadecimal.
