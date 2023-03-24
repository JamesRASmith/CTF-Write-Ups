# Trapped Source

## Challenge Solution

This was the first challenge within the Cyber Apocalypse 2023 CTF event.

This challenge gave me a docker to spawn, so that was my first step to bring the challenge online

![image](https://user-images.githubusercontent.com/57868272/227614753-a5b3f9a1-7ba6-455e-a198-160fd6fada3b.png)

Loading the challenge, I was given a lock that required a 4 number pin to unlock. After attempting the obvious combination of '1234' (and this not solving the challenge) I decided to check the page source of the challenge, as this is often the first step within Web challenges to check for any easy information that can be found.

![image](https://user-images.githubusercontent.com/57868272/227615693-da9af3cb-efd1-4daf-8ec0-5b39624bfb9f.png)

Right at the top of the page source I found the above code. This shows that the correct pin to solve the challenge is '8291'. Putting this into the pin I was greeted with the following flag.

![image](https://user-images.githubusercontent.com/57868272/227616222-92419f59-fbe1-456c-85db-e1f73f2a8610.png)

With this being the first challenge in the WEB challenges I expected that this would be a simple challenge to solve! 

Below I explain quickly how to remediate this.

## Challenge Remediation

Remediation of this challenge would be simple to complete, it would simply require a developer to remove the above seen code, this would a hotfix to resolve the issue ASAP.

A long term solution to avoid this happening in the future would be to implement checks such as peer reviews before code is moved from the development/staging environments and pushed out to the production environment. A simple check such as this goes a long way to help avoid issues such as this arising and can be easily implemented through the use of Github issues (allowing for paper trails to be kept for changes) other software is likely available, however I only have experience in using Github myself.
