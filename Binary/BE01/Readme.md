# Briefing
> Download the file and find a way to get the flag.
Contents: chicken.pdf

## Solution
Using Binwalk, extract any embeded files

```console
binwalk -e chicken.pdf

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PDF document, version: "1.4"
72            0x48            Zip archive data, at least v1.0 to extract, compressed size: 550522, uncompressed size: 550522, name: egg.zip
550609        0x866D1         End of Zip archive, footer length: 22
551319        0x86997         Zlib compressed data, default compression
6478358       0x62DA16        Zlib compressed data, default compression
6478601       0x62DB09        End of Zip archive, footer length: 22


```

Output of extraction: egg.zip --> chicken.zip --> egg.zip --> chicken.zip --> egg.pdf

## Flag
Flag: wh1ch_came_f1rst?


