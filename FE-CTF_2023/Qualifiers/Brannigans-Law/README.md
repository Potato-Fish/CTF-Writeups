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

First we are told: "The seyvaan-siipians expect a file called "