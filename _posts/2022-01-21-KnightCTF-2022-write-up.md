## KnightCTF - 2022 Write-up

I'll take you with this write-up through some of the challenges I've solved during KnightCTF-2022. 

The CTF was beginner-friendly with some challenges being a bit harder than others.

Big ups for all the team that worked on this ctf.

---

### Starters 

During this CTF, i've chosen to publish write-ups for Networking, OSINT, Web, and some other challenges here-and-there.

---

### Networking
This was the part that i enjoyed most during this CTF, multiple challenges were related and worked on the same file which you found on the following challenge.

#### Compromised CTF Platform

![Compromised_CTF_Platform](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Compromised_CTF_Platform?raw=true)

This challenge starts by giving you a network capture and asks you to find the username and password that the hacker found. 
After downloading the file "traffic.pcapng", you'll need to open it with the most famous network protocol analyzer "Wireshark".

![Compromised_CTF_Platform1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Compromised_CTF_Platform1?raw=true)

Opening the file will reveal multiple packets that were captured, the files used different protocols but an interesting one here is HTTP, which is known for being insecure as opposed to HTTPS its follower.

Furthermore, what's interesting in the HTTP files is the fact that that we can see what the user sent to the server using the POST method in plain text. 

And for this challenge, if you cycle through the POST requests you'll find this pair of credentials : 

![Compromised_CTF_Platform2](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Compromised_CTF_Platform2?raw=true)

Then, using the flag <b>KCTF{demo_demo}</b> will solve the challenge

---

#### Admin Arena 

![Admin_Arena](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Admin_Arena?raw=true)

I've listed this challenge right after the Compromised CTF Platform for a reason, and the reason is that i found the flag for this one while solving the first challenge. 

![Admin_Arena1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Admin_Arena1?raw=true)

Using the mail address and the password then putting them in the right format will give you the flag for this challenge.

---

#### FTP Flag

![FTP_Flag](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/FTP_Flag?raw=true)

As the name of this challenge suggests, we're capturing the packets using the FTP protocol this time.
Doing it the same way as with HTTP, typing FTP in the filter will work just fine for us.
Then cycling through the packets, we find an interesting one : 

![FTP_Flag1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/FTP_Flag1?raw=true)

The user here used the RETR command which is used to take a make a copy of a file. But the thing here is that, we don't see the file or the repsponse from the server. In order to do that, since the server doesn't use the FTP protocol to send the file back, we have to remove the filter that we applied previously. But before we do that, you have to remmember the packet's number (7312).

![FTP_Flag2](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/FTP_Flag2?raw=true)

If we look at the server's response, we find a base64 encoded string. Decode this string using CyberChef and you'll find yourself the flag for this challenge.

---

#### Robots.txt

![Robots.txt](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Robots.txt.png?raw=true)

This will be the last challenge related to the "traffic.pcapng" file and the last challenge in the Networking category.
As the challenge said, we're looking for the file "Robots.txt", this link was probably also accessed using http, so all we have to do is to apply http as a filter and look for when the user accessed this directory.

![Robots.txt1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Robots.txt1.png?raw=true)

After finding the request, we look for the server's reply which is 2 packets after it. You'll just need to take the file path and put it in the flag format.

---

### OSINT

#### Canada Server 

![Canada_Server](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Canada_Server.png?raw=true)

The first intuition for everyone will be to visit the mentioned company's website. After doing so, you can either look in server if you find information about the company's servers (I didn't do that) or simply copy the domain name of the company's site and paste it in a DNS Resolver, i used the first option i found on google which was this one : 

![Canada_Server1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Canada_Server1.png?raw=true)

Simply take the ip address and put it in the flag's format, and there you have the solution for this challenge.

#### Explosion In Front Of Bank Of Spain

![Explosion_In_Front_Of_Bank_Of_Spain](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Explosion_In_Front_Of_Bank_Of_Spain.png?raw=true)

This challenge starts by giving you the following image : 

![Explosion_In_Front_Of_Bank_Of_Spain1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Explosion_In_Front_Of_Bank_Of_Spain1.png?raw=true)

As a first step to this challenge, you should check all of its details and do the usual check. Although this time you'll find nothing. One step further, putting it in Google Image Search will show you that this was a picture taking from the TV Series "La Casa De Papel". Some more research and you'll find that this scene was filmed in front of the "Ministerio de Fomento en Madrid". Google Maps then should be your friend and you'll find the coordinates of this location that will give you your flag.

#### Find The Camera

![Find_the_Camera](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Find_The_Camera.png?raw=true)

Another OSINT challenge and another Google Search, If you search for the Copyrights on the Image, JenCh012, you'll find your Image and deeper search will get you to this site : 

![Find_the_Camera1](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Find The Camera1.png?raw=true)

Look up for the DSC-S980 model and you'll find out that it's a Sony Camera, put the information you've collected in the Flag format and boom you're done.

![Admin_Arena](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/2022-01-21-KnightCTF-2022-write-up/Admin_Arena.png?raw=true)