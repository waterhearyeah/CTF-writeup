# Flag Hunters

>Author: syreal  
>Description 
>Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it? There might be something in it for you.  
>The program's source code can be downloaded here.  
>Connect to the program with netcat:  
>$ nc verbal-sleep.picoctf.net 56688

## From the source code provided

```python
import re #library that working with regular expressions, can search, match, and manipulate strings based on patterns
import time


# Read in flag from file  
flag = open('flag.txt', 'r').read()

secret_intro = \
'''Pico warriors rising, puzzles laid bare,
Solving each challenge with precision and flair.
With unity and skill, flags we deliver,
The ether’s ours to conquer, '''\
+ flag + '\n' #From here, learnt that the flag is hidden in this part


song_flag_hunters = secret_intro +\ #This variable need to be triggled 
'''

```
