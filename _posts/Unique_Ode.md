## Unique Ode Virtual Machine

This writeup will cover the virtual machine that i developed named "Unique Ode"

The code that i wrote to develop this machine is linked in this github repository : https://github.com/eobeob10/Unique_ode_data.git


The ip for the machine is : 137.117.214.77

--- 

Like any other machine, we should start this machine by running an nmap scan, after running the nmap with default scripts ( -sC ) and enumerating versions ( -sV ) :

```bash
nmap -sC -sV 137.117.214.77
```


The nmap command returns this :

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/1.png?raw=true)


We see that 2 ports are open : ssh and ftp

We also see that anonymous login is available on the ftp service.

Let's check what's available on this ftp server.

```bash
ftp 137.117.214.77
```

Username = "anonymous", Password = ""

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/2.png?raw=true)


```bash
ls
get flag.txt
```
![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/3.png?raw=true)


We find a flag on the machine, we download it and cat it only to find out that it is a fake flag ! 

We then ftp back to the machine, and instead of running a normal ls command we run :

```bash
ls -la
cd .data
get hmmm
```

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/5.png?raw=true)

This hmmm file contains a crypted data. But what's weird about it is that it starts with a <b> o' </b> and ends with a <b>==</b>.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/6.png?raw=true)

First intuition is to base64 decode it.

Using python and running this command : 

```python
import base64
base64.b64decode("<DATA>")
```

But we know that the input is not valid base64 encoding.

Noticing the ' and the == we know that these characters don't get shifted by a normal rot. After we rot13 this data we get a new string.

We notice that the string now starts with <b>b'</b>, which is the notation that python uses for bytes. 

Now decoding the string with base 64, doesn't give us any readable data, but knowing that it's python bytes, it may actually be a python pickle.

Running the following commands :

```python
import base64
import pickle
pickle.loads(base64.b64decode("<DATA>"))
```
We get the following List of tuples : 

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/7.png?raw=true)


We notice that there is a pattern in these elements, some of them starting with either p or u then followed by another letter, grouping these elements in the following order : ua + ub + uc .., pa + pb + pc .., we get the following strings : 

<b>Pindaric</b>
<b>Stesich0ru5_R0cK5</b>

These seem like Credentials for the user "Pindaric", let's try to ssh in the machine using these credentials 

```bash
ssh Pindaric@137.117.214.77
```

We get in !

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/8.png?raw=true)

Checking our home directory, we find out that it's empty, we go then to check the other user's home directories.

We find in it a user.txt file that we can cat to get the first flag and another folder named unique_ode that we can't access. We know that we have to switch to this Horatian user.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/9.png?raw=true)

Checking the hidden directories in the home directory we find a .ssh directory.

We change to that directory and find that this user's private key is readable.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/10.png?raw=true)

We take that key and use it to log into the Horatian user.

```bash
ssh -i id_rsa Horatian@137.117.214.77
```
![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/11.png?raw=true)

We successfully log in as the Horatian user.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/12.png?raw=true)

After that, we want to escelate our privileges and become the root user. To do so, we run the following command as basic privilege escalation default scan :

```bash
sudo -l
```
![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/13.png?raw=true)

We find that Horatian can run the binary /home/unique_ode/unique_ode as the root user.

Trying to run this binary we get a small challenge. 

The program is asking us to repeat what it's outputting, doing so, we get through the first challenge, but the program exits when we type the 2nd telling us that we're using illegal characters.

By reference to the machine's name, we should probably try to input the characters using Unicode.
Trying to Convert the characters to Unicode, we get through for the second and third challenge : 

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/14.png?raw=true)

When we finish the challenges we're told we're welcome to the uniquoders club, But every character that's not written in unicode ends up displaying an error. 

We convert our commands to unicode and try to ls the root directory.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/15.png?raw=true)

We are ROOT !

Then, we can probably cat the flag that's in the root directory. But when we try to, the system says it doesn't recognize the root.txt file.

We could either notice that the start of the file's name starts with an extra space, and cat it using the following command : cat /root/${\u2000root.txt} or just cat everything in the root directory using the command : cat /root/*.

![Unique_Ode](https://github.com/eobeob10/eobeob10.github.io/blob/main/_posts/unique_ode/16.png?raw=true)




