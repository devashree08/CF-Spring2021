# Briefing
> Download the file and find a way to get the flag.
> Contents: flag

## Solution
What we get when we run the flag file
``` console
/home/dev/Downloads/flag

 Flag:
       __       __                          _                      ____ __           
  ____/ /___   / /_   __  __ ____ _ ____ _ (_)____   ____ _       / __// /_ _      __
 Error displaying rest of flag
```
Analyze the file in Ghidra
> see the picture for output
``` console
int main(void)

{
  int rows;
  int cols;
  
  fflush(stdout);
  puts("\n\x1b[36m Flag:\x1b[0m");
  output(2,0x55);
  return 0;
}
.
.
.

if (rows < 6) {
    puts("\x1b[31m Error displaying rest of flag\x1b[0m");
  }
  ```

```console
pwndbg> b main
Breakpoint 1 at 0x8d5: file flag.c, line 30.
pwndbg> r
Starting program: /home/dev/Downloads/flag 
ERROR: Could not find ELF base!

Breakpoint 1, main () at flag.c:30
30      flag.c: No such file or directory.
LEGEND: STACK | HEAP | CODE | DATA | RWX | RODATA
──────────────────────────────────────────────────────────────────────────────[ REGISTERS ]───────────────────────────────────────────────────────────────────────────────
 RAX  0x5555555548cd (main) ◂— push   rbp
 RBX  0x0
 RCX  0x7ffff7fab718 (__exit_funcs) —▸ 0x7ffff7fadb00 (initial) ◂— 0x0
 RDX  0x7fffffffe0f8 —▸ 0x7fffffffe417 ◂— 'COLORFGBG=15;0'
 RDI  0x1
 RSI  0x7fffffffe0e8 —▸ 0x7fffffffe3fe ◂— '/home/dev/Downloads/flag'
 R8   0x0
 R9   0x7ffff7fe2180 (_dl_fini) ◂— push   rbp
 R10  0x0
 R11  0xc2
 R12  0x555555554680 (_start) ◂— xor    ebp, ebp
 R13  0x0
 R14  0x0
 R15  0x0
 RBP  0x7fffffffdff0 —▸ 0x555555554920 (__libc_csu_init) ◂— push   r15
 RSP  0x7fffffffdfe0 —▸ 0x7fffffffe0e0 ◂— 0x1
 RIP  0x5555555548d5 (main+8) ◂— mov    rax, qword ptr [rip + 0x201734]
────────────────────────────────────────────────────────────────────────────────[ DISASM ]────────────────────────────────────────────────────────────────────────────────
 ► 0x5555555548d5 <main+8>     mov    rax, qword ptr [rip + 0x201734]
   0x5555555548dc <main+15>    mov    rdi, rax
   0x5555555548df <main+18>    call   fflush@plt <fflush@plt>
 
   0x5555555548e4 <main+23>    lea    rdi, [rip + 0x90d]
   0x5555555548eb <main+30>    call   puts@plt <puts@plt>
 
   0x5555555548f0 <main+35>    mov    dword ptr [rbp - 8], 2
   0x5555555548f7 <main+42>    mov    dword ptr [rbp - 4], 0x55
   0x5555555548fe <main+49>    mov    edx, dword ptr [rbp - 4]
   0x555555554901 <main+52>    mov    eax, dword ptr [rbp - 8]
   0x555555554904 <main+55>    mov    esi, edx
   0x555555554906 <main+57>    mov    edi, eax
────────────────────────────────────────────────────────────────────────────────[ STACK ]─────────────────────────────────────────────────────────────────────────────────
00:0000│ rsp 0x7fffffffdfe0 —▸ 0x7fffffffe0e0 ◂— 0x1
01:0008│     0x7fffffffdfe8 ◂— 0x0
02:0010│ rbp 0x7fffffffdff0 —▸ 0x555555554920 (__libc_csu_init) ◂— push   r15
03:0018│     0x7fffffffdff8 —▸ 0x7ffff7e13d0a (__libc_start_main+234) ◂— mov    edi, eax
04:0020│     0x7fffffffe000 —▸ 0x7fffffffe0e8 —▸ 0x7fffffffe3fe ◂— '/home/dev/Downloads/flag'
05:0028│     0x7fffffffe008 ◂— 0x100000000
06:0030│     0x7fffffffe010 —▸ 0x5555555548cd (main) ◂— push   rbp
07:0038│     0x7fffffffe018 —▸ 0x7ffff7e137cf (init_cacheinfo+287) ◂— mov    rbp, rax
──────────────────────────────────────────────────────────────────────────────[ BACKTRACE ]───────────────────────────────────────────────────────────────────────────────
 ► f 0   0x5555555548d5 main+8
   f 1   0x7ffff7e13d0a __libc_start_main+234
──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
pwndbg> p output(6,0x55)
       __       __                          _                      ____ __           
  ____/ /___   / /_   __  __ ____ _ ____ _ (_)____   ____ _       / __// /_ _      __
 / __  // _ \ / __ \ / / / // __ `// __ `// // __ \ / __ `/      / /_ / __/| | /| / /
/ /_/ //  __// /_/ // /_/ // /_/ // /_/ // // / / // /_/ /      / __// /_  | |/ |/ / 
\__,_/ \___//_.___/ \__,_/ \__, / \__, //_//_/ /_/ \__, /______/_/   \__/  |__/|__/  
                          /____/ /____/           /____//_____/                      
$1 = void
```

## Flag
Flag; debugging_ftw
