# Timed Transmission

![image](https://user-images.githubusercontent.com/57868272/229302434-0e7974e6-37ec-4cb2-a3b0-d0215f37eb06.png)

In this challenge I was given a number of files to download, one of these was a '.sal' file type (something I haven't come across before) A quick look online shows that they appear to be related to data transmission over serial ports.

I decided my first step should be to review one of the 'bin' that was downloaded to see if this had any pointers as to what my next step should be.

![image](https://user-images.githubusercontent.com/57868272/229302453-74a1dabe-6426-4e6c-b906-44b286cb663f.png)

Opening the .bin files in the terminal showed that each file started with the string '<SALEAE>'. Google showed that this appeared to be a company that creates logic analysers and software that can be used to '.sal' files!

![image](https://user-images.githubusercontent.com/57868272/229302578-23fd2966-fa42-4bf8-b2a5-c9954b5b3dd7.png)

I decided to download the Logic2 program onto my Kali Linux box and see if it was of any use in solving this problem. Opening the 'Captured Signals.sal' file I was greeted with an expanded view of the signals and decided to zoom into the signals to get a more expanded view.

![image](https://user-images.githubusercontent.com/57868272/229302760-f81c229b-016a-4088-bb2a-47a5a121e89e.png)

It was whilst playing around zooming into the signals that I noticed the start of the signals appeared to represent the characters 'HTB'. This resulted in me not zooming any fruther in or out and then working through the file to find the entire string. The image above is simply a snapshot of the entire flag for the challenge!
