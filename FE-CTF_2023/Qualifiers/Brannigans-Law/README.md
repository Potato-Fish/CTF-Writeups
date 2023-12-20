# Brannigan's Law

## Description
*Captain Zip Brannigan at your service!*

*Stardate... April. The 13th. Point two.*

*We've made it to Kompromaise 7, the have-it-both-ways world.*

*Everyone here, from young to old, and in between (..especially in between) are used to compromising.*

*It. Disgusts. Me.*

*But fear not! I have assigned my most trusted chump^H^H^H^H^Hdiplomatic envoy to help make contact.*

*That's YOU!*

*You need to send a zip file to initiate first contact.*

*Now remember, the younger seyvaan-siip people, and the older, more conservative ohns-ehp people don't get along.*

*Please send a single file that makes everybody happy. And no excuses!*

*What are you waiting for, cadet? Fly over to brannigans-law.hack.fe-ctf.dk:1337 right away.*

*Brannigan out!*

## Solution
As is somewhat pointed out in the rambling description, we want to send a zip file, that when unziped will provide one result for the "seyvaan-siip people", and another for the "ohns-ehp people". But how is this possible???

To start of with, we created a python script that connects to the server at 'brannigans-law.hack.fe-ctf.dk:1337'. A lot of time was used fiddeling with recieving data from the server, and  how to send files to the remote host. Luckily, we get a lot of feedback when we connect to the host.

First we are told: "*The seyvaan-siipians expect a file called* ", and then a random string of text, as well as what the file should contain.<br>
We are also told: "*But the proud ohns-ehp tribe demand a file called* ", also with a random string, and the expected file contents.

We are then asked to provide the length of a zip file, as well as the zip file itself.




```Python
from pwn import *
import subprocess
from os import system

context.log_level = 'DEBUG'

r = remote("brannigans-law.hack.fe-ctf.dk", 1337)

r.recvuntil(b'The seyvaan-siipians expect a file called ')
msg1 = r.recvuntil(b'\n')
r.recvuntil(b'But the proud ohns-ehp tribe demand a file called ')
msg2 = r.recvuntil(b'\n')

file_name1 = msg1.split(b"'")[1].decode()
content1 = msg1.split(b"'")[3].decode()


file_name2 = msg2.split(b"'")[1].decode()
content2 = msg2.split(b"'")[3].decode()

with open(file_name1, 'w') as f1, open(file_name2, 'w') as f2:
    f1.write(content1)
    f2.write("")

# Check if files.zip exists, and if so, delete it
if os.path.exists('files.zip'):
    os.remove('files.zip')
if os.path.exists('combined.zip'):
    os.remove('combined.zip')

subprocess.run(['7z', 'a', 'files.zip', file_name1, file_name2],
               stdout=subprocess.DEVNULL, 
               stderr=subprocess.DEVNULL
               )

os.remove(file_name1)
os.remove(file_name2)
with open(file_name2, 'w') as f2:
    f2.write(content2)


subprocess.run(['7z', 'a', 'files2.zip', file_name2],
               stdout=subprocess.DEVNULL, 
               stderr=subprocess.DEVNULL
               )

os.system("cat files.zip files2.zip > rename_me.zip")
os.system("zip -F rename_me.zip --out combined.zip")

sleep(1)
try:
    os.remove(file_name1)
    os.remove(file_name2)
    os.remove("files2.zip")
    os.remove("files.zip")
    os.remove("rename_me.zip")
except:
    pass

with open("combined.zip", "rb") as f:
    data = f.read()
r.recvuntil(b'Cadet. How large is this file of yours going to be?\n')
r.send((str(len(data))+"\n").encode())
r.recvuntil(b'Receiving file..')
r.send(data)
r.interactive()
```



The server uses “7z” to extract the first two files made for “seyvaan-siip” people, and make sure they contain the expected data and names. Then it will use “unzip” to extract the one file for “ohns-ehp”, and fail on the first file (wrong file), which it is ment to in this case, and again check these for the expected data and names.

When these tests are done, and all are passed, we get the flag:

<details>
  <summary>FLAG</summary>
  flag{i_dont_pretend_to_understand_brannigans_law_i_merely_enforce_it}
</details>
