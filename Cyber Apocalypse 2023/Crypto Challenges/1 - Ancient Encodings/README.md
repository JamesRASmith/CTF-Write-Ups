# Ancient Encodings

It pains me to say that I didn't realise that Crypto and Forensics were a part of this CTF, until 2 days into the CTF (definitely cost me some points)
This was simply due to me just missing the 'Show More' button on the screen due to a dark mode extension I was using at the time.

With that shameful disclaimer out of the way, in this challenge I was given the below files and was asked to create a script that would counter the encryption applied to the flag

![image](https://user-images.githubusercontent.com/57868272/229303169-a37c41f6-80dd-4762-a3da-6e9dfbf3e76c.png)

![image](https://user-images.githubusercontent.com/57868272/229303394-09b83bc5-8b9e-4f6c-a9d2-1d11377c39df.png)

Opening the above 'source.py' file I was greeted with a simple Python script that took a string assigned it to the variable 'FLAG' and then the string is converted from bytes to a long integer and is then encoded using base 64. This encoded string is then output to the file 'output.txt' Reviewing write-ups for previous PWN challenges this is often a challenge that is provided at the start of events such as this.

As the code was written in Python it made it easier for me to write my own script that could solve this challenge. Instead of saving this in a file, I decided to use the Python Interpreter via the terminal to save time.

![image](https://user-images.githubusercontent.com/57868272/229303466-eb2f0927-aec3-4aa9-956c-7b5b6ee297f0.png)

I first imported the required libraries to decode the string provided and get the flag.

![image](https://user-images.githubusercontent.com/57868272/229303551-e86b2af1-bece-49ec-946c-bb8104fd8a31.png)

I then copied the encoded flag from the 'output.txt' file and assigned this to the variable 'encoded_flag' for later use. I also stripped this string to avoid any whitespaces causing issues later in the program.

![image](https://user-images.githubusercontent.com/57868272/229303693-dad78ab2-251d-4496-9307-1294e7741186.png)

This is where the encoded flag is now actuall decoded and can then be printed to the console.

The first line in the above image converts the string assigned to 'encoded_flag' to an integer with a base of 16. I used base 16 here as the string seen earlier contains hexadecimal values and this is BASE 16.

With the string now converted to an integer I now converted the string from a long integer back into bytes. This is done through the function 'long_to_bytes' and assigned to the variable 'decoded_bytes'.

Finally, the string can now be decoded using the base 64 library and the value assigned to the variable 'flag'.

The whole script and flag can be seen below!

![image](https://user-images.githubusercontent.com/57868272/229303964-62263a7c-640f-488e-b277-aac08cbe5ff4.png)
