# Briefing
> Download the file and find a way to get the flag.
Contents: chicken.pdf

## Solution
Using Binwalk, extract any embeded files

```console
binwalk -e chicken.pdf


```

Output of extraction: egg.zip --> chicken.zip --> egg.zip --> chicken.zip --> egg.pdf

## Flag
Flag: wh1ch_came_f1rst?


