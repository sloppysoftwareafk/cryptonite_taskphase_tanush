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

