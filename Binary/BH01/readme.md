# Briefing
> Download the file and find a way to get the flag.
> Contents: program

## Solution
What we get when we first run the program:
``` console
$ /home/dev/Downloads/program                                                                                                           
What is the magic word?
What is the magic workd
Flag: aLittLeObfuScatIonalChauF?9��▒
Did you understand that?
```
Ghindra output:
```
  char input_char;
  uint iter;
  int random;
  time_t curr_time;
  byte indexes [5];
  char input [40];
  char flag [8];

  curr_time = time();
  srand((uint)curr_time);
  memset(input, 0, sizeof input);
  indexes = [0x16, 0x12, 0x0a, 0x05, 0x18];
  puts("What is the magic word?");
  fflush(stdout);
  fgets(input,0x28,stdin);
  flag = 0x103f4f6c803a05b6;
  random = rand();
  input_char = input[(int)indexes[random % 5]];
  iter = 0;
  while (iter < (int)input_char - 0x5a) {
    [ OBFUSCATED FLAG GEN ]
    if ((int)((int)input_char - 0x5a) < 0) break;
    [ OBFUSCATED FLAG GEN ]
    iter = iter + 1;
  }
  puts(flag);
  puts("Did you understand that?");
  ```
The binary picks a random number between 0 and 4 inclusive, and then looks up that index in the `indexes` array. 
It then uses that value to index your input, subtracts hex `5a` (decimal 90), and will iterate through the while loop that many times.

At this point, I realised why I was getting different behaviour when I put 16 or so "h"s in. 
If the random index picked was less than 16, then the while loop would execute ord("h") - 90 (14) times, 
and checking the output of the program it looked like I was getting 14 characters of human-readable flag out!

So. I need to make that while loop run as long as possible, and I need to provide enough bytes of input so that any random index 
it could pick would still hit the byte of input that I provided (and not \x00, if I had not provided that much input). 
The input buffer is 40 long, so I wrote a quick python oneliner to generate the payload for me.

Sure enough, the result each time of running that is the same and no longer affected by the time-seeded-random aspect. 
As I tried i, then j, as expected I got one more character of flag output at a time. I kept working my way down the ASCII table, until eventually:

```
➜ ~ $ python -c "print('~'*40)" | ./program
What is the magic word?
Flag: aLittLeObfuScatIonalCharActEr
Did you understand that?
```

## Flag
aLittLeObfuScatIonalCharActEr
