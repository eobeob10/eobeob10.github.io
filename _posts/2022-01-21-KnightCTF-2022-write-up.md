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

<img src = "/2022-01-21-KnightCTF-2022-write-up/Compromised CTF Platform.png" style="float: left; margin-right: 10px;">

This challenge starts by giving you a network capture and asks you to find the username and password that the hacker found. 
After downloading the file "traffic.pcapng", you'll need to open it with the most famous network protocol analyzer "Wireshark".

<img src = "/2022-01-21-KnightCTF-2022-write-up/Compromised CTF Platform1.png" style="float: left; margin-right: 10px;">

Opening the file will reveal multiple packets that were captured, the files used different protocols but an interesting one here is HTTP, which is known for being insecure as opposed to HTTPS its follower.

Furthermore, what's interesting in the HTTP files is the fact that that we can see what the user sent to the server using the POST method in plain text. 

And for this challenge, if you cycle through the POST requests you'll find this pair of credentials : 

<img src = "/2022-01-21-KnightCTF-2022-write-up/Compromised CTF Platform2.png" style="float: left; margin-right: 10px;">

Then, using the flag <b>KCTF{demo_demo}</b> will solve the challenge

---

#### Admin Arena 

<img src = "/2022-01-21-KnightCTF-2022-write-up/Admin Arena.png" style="float: left; margin-right: 10px;">

I've listed this challenge right after the Compromised CTF Platform for a reason, and the reason is that i found the flag for this one while solving the first challenge. 

<img src = "/2022-01-21-KnightCTF-2022-write-up/Admin Arena1.png" style="float: left; margin-right: 10px;">

Using the mail adress and the password then putting them in the right format will give you the flag for this challenge.

---

#### FTP Flag

<img src = "/2022-01-21-KnightCTF-2022-write-up/FTP Flag.png" style="float: left; margin-right: 10px;">

As the name of this challenge suggests, we're capturing the packets using the FTP protocol this time.
Doing it the same way as with HTTP, typing FTP in the filter will work just fine for us.
Then cycling through the packets, we find an interesting one : 

<img src = "/2022-01-21-KnightCTF-2022-write-up/FTP Flag1.png" style="float: left; margin-right: 10px;">

The user here used the RETR command which is used to take a make a copy of a file. But the thing here is that, we don't see the file or the repsponse from the server. In order to do that, since the server doesn't use the FTP protocol to send the file back, we have to remove the filter that we applied previously. But before we do that, you have to remmember the packet's number (7312).

<img src = "/2022-01-21-KnightCTF-2022-write-up/FTP Flag2.png" style="float: left; margin-right: 10px;">

If we look at the server's response, we find a base64 encoded string. Decode this string using CyberChef and you'll find yourself the flag for this challenge.

