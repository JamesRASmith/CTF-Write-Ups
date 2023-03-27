# Shattered Tablet

This was the first reverse challenge within the 2023 Cyber Apocalypse event and my first real attempt at an active reverse challenge without the assistance of a write-up or youtube video.

As with many Reverse engineering challenges I was given a binary to download and simply had to go from there!

![image](https://user-images.githubusercontent.com/57868272/228025676-c8275588-4810-497c-95d5-9efec471a04f.png)

As this was my first actual attempt at reverse engineering a binary, I was still working out my own order to carry out my checks, but eventually settled on the following.

![image](https://user-images.githubusercontent.com/57868272/228026073-0d13128f-e66e-4c85-973a-1b282f77d0ca.png)

My first step was to check the security settings associated with the binary, from this screenshot I can gather the following information:

**Canary** - This tells me that the binary does NOT have a canary present and this is not something that I need to worry about! In later challenges this may be present and would mean that should the canary value be changed in anyway the binary would stop execution immediately (often used as protection against buffer overflow)

**NX** - This being enabled simply means that the memory segments cannot be BOTH writeable and executable. This is useful as writeable memory should never be executed as it can be manipulated.

**PIE** - This being enabled means that the program does not tell the loader which virtual address to use and therefore the addresses used can vary, this makes memory based attacks more difficult to accomplish!

With this information noted I could continue with the challenge

![image](https://user-images.githubusercontent.com/57868272/228028409-8badf367-d33d-4d1a-9d55-38119692ed3f.png)

I used the 'file' command to also quickly grab some information BEFORE opening the binary in Ghidra. From this I can see that the binary is not stripped (this makes reversing the binary much easier)

![image](https://user-images.githubusercontent.com/57868272/228028730-c2e8dcdc-b659-4cd8-80ec-795517ca255f.png)

My final check (for a quick win) was to check the output of the strings command for the flag of the challenge, as you can see this was not the case in this challenge.

With the basic checks completed I decided to move onto actually opening the binary within Ghidra!

![image](https://user-images.githubusercontent.com/57868272/228033892-2b1d28c4-ea01-45f7-a59c-088380d92fb3.png)

The first step is to locate the 'main' function as this is where the binary will start from (in my experience at least.) Once I had located the main function I was greeted with the following code.

![image](https://user-images.githubusercontent.com/57868272/228034259-8250f7e6-8737-4229-89b6-62accfa6f432.png)

When reviewing the code I noted that the variables 48-28 all appeared to have their a variable that was labelled as such ``` ((char)local_48 == 'H')) ``` this combined with the fact that all flags within HTB CTF's and machines begin with the string 'HTB{' made me inclined to believe that I simply had to put the above mess of characters into an order that represented the flag.

My first step was to locate the following 3 characters 'HTB', luckily for me these characters were only present once, these were noted as follows:

```
((char)local_48 == 'H'))
(local_48._1_1_ == 'T'))
(local_48._2_1_ == 'B'))
```

Can you see the pattern for each of these?

Once aligned the code mentions that the next character in the flag is essentially +1 to the previous character. So for example the flag begins with a capital H, then T = local_48._1_1 and B = local_48._2_1. It would appear that the numbers are ordered based off the order of the variables when first defined:

![image](https://user-images.githubusercontent.com/57868272/228036032-5212ca55-6866-4d9e-bd1f-531e815feab7.png)

And they are then further organised based on the numerical value after the variable name (starting with the character defined in the (char) value.

I proceeded to spend the next few minutes working through the tangle of characters on this hypothesis and was eventually greeted with the following flag!

HTB{br0k3n_4p4rt,n3ver_t0_b3_r3p41r3d}
