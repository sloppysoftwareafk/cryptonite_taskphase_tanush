# Binary Exploitation

## Print the Gifts

We begin with interacting with the program.

![image](/content/nitectf_binaryexp_printthegifts_1.png)

We understand that it prints the given input so we search for a format string vulenrability.

My first approach was to pass special characters to guess the input/output functions.

![image](/content/nitectf_binaryexp_printthegifts_2.png)

Since this doesn't yield any helpful output as seen, I researched about binary vulnerabilities.
This led me to check for them using format string specifiers.

![image](/content/nitectf_binaryexp_printthegifts_3.png)

To confirm any input prompt vulnerability we use `%p %x %s`.

![image](/content/nitectf_binaryexp_printthegifts_4.png)

Note : This is called the fuzz input method.
<br>
The outputs to these look like standard addresses.
This can be used to leak the stack and libc addresses.
After looking into this, I tried geting the offsets of the addresses.

![image](/content/nitectf_binaryexp_printthegifts_5.png)

