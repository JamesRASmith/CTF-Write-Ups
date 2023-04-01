# Plaintext Treasure

This was the first challenge in the forensics category of the CTF.

![image](https://user-images.githubusercontent.com/57868272/229304189-7a2694d0-dc07-4ff5-95dd-fc45099e25f5.png)

As always I was given some files to download, in this challenge this was a .zip file that contained a pcap file, a file type that can be opened in Wireshark and network traffic can then be analysed.

![image](https://user-images.githubusercontent.com/57868272/229304278-b4fe56c9-d421-468e-800b-1b0264bc4a33.png)

I booted up Wireshark and opened the file up and decided the best first step should be to check the Protocol Hierarchy Statistics for the captured traffic as a whole. As you can see this file contains only TCP packets and most of these appear to be HTTP packets. This is where I should begin my investigation.

![image](https://user-images.githubusercontent.com/57868272/229304641-6a8622f6-77dc-4bc5-82b1-c8bf8e13117d.png)

As I have some past experience using Wireshark, I decided to simply look for the flag as soon as possible rather than first familiarising myself with the software. To cross off any quick wind I decided I would check the first 10 TCP streams for the string 'HTB'.

![image](https://user-images.githubusercontent.com/57868272/229304654-30d2bef1-026f-468d-8f3e-34dc3854ba09.png)

When I reached TCP stream 4 I found the above flag for the challenge!
