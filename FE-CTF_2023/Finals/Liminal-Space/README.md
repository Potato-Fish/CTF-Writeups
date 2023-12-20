# Liminal Space

## Description
*We've intercepted this... thing. I have no idea.
I sent it to the people in the lab, and they said the file was empty, with a blank stare. Then they asked me to pay!
"Just put it on my tab", I told them. So I'm giving them a wide berth. They need their space.
We need a new line of inquiry. Maybe you can help?*

## Challenge
The challenge and it's files can be found here: https://github.com/FE-CTF/2023/tree/master/finals/challenges/liminal-spaces


## Solution
At a first glance, the file just looks like it contains nothing, but opening it with some IDEs, you can see that there are a lot of newlines, returns and spaces. This is a clear indicator of the esoteric programming language know as 'Whitespace'. (I saw a video about coding languages a while back and remember it from this. https://youtu.be/gwLQMuTspxE?t=1987)'

As this language is esoteric, there aren't very many interpreters for this language, and it cant really be compiled. I tried using different tools on github in an attempt to translate it or compile it, but nothing would work. On the other hand I could find some online interpreters that would run the code and see that I would be prompted for a password, and that got me thinking. "If it prints text, maybe there is a way to find all the characters that this program would output (by the sequence of characters representative of outputting a character), and in that, there might be the flag". So, with nothing to find online, I asked Hannes for some help from his GPT4. This output the strings, but the flag was not in this, and by this time, the competition ended. I later looked back, and looked at what code it was generating in order to get the strings.
