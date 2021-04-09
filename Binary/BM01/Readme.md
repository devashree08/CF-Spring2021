# Briefing
> Download the file and find a way to get the flag.
> Contents: program

## Solution
``` console
/home/dev/Downloads/program
Какой пароль？
> 
неверный.
```
To find the password, run the program through GDB using `gdb ./program`.
From `info func`, we can see there is a main function so set a breakpoint by doing `b main`.
``` console
 ► 0x55555555482f <main+101>    call   strcmp@plt <strcmp@plt>
        s1: 0x5555555549c8 ◂— 0xbed0bbd0bed0bcd0
        s2: 0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */

----------------x------------------------x---------------------------x------------------------x---------------------------x
  
pwndbg> next
0x000055555555482f in main ()
LEGEND: STACK | HEAP | CODE | DATA | RWX | RODATA
───────────────────────────────────────────────────────────────[ REGISTERS ]───────────────────────────────────────────────────────────────
 RAX  0x5555555549c8 ◂— sar    byte ptr [rax + rdx*8 - 0x2f442f42], 1
 RBX  0x0
 RCX  0x7ffff7edbe8e (read+14) ◂— cmp    rax, -0x1000 /* 'H=' */
 RDX  0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */
*RDI  0x5555555549c8 ◂— sar    byte ptr [rax + rdx*8 - 0x2f442f42], 1
 RSI  0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */
 R8   0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */
 R9   0x7ffff7fabbe0 (main_arena+96) —▸ 0x555555756ab0 ◂— 0x0
 R10  0x6e
 R11  0x246
 R12  0x5555555546c0 (_start) ◂— xor    ebp, ebp
 R13  0x0
 R14  0x0
 R15  0x0
 RBP  0x7fffffffdff0 —▸ 0x555555554940 (__libc_csu_init) ◂— push   r15
 RSP  0x7fffffffdf80 ◂— 0x0
*RIP  0x55555555482f (main+101) ◂— call   0x5555555546a0
────────────────────────────────────────────────────────────────[ DISASM ]─────────────────────────────────────────────────────────────────
   0x55555555481c <main+82>     call   fgets@plt <fgets@plt>
 
   0x555555554821 <main+87>     lea    rdx, [rbp - 0x50]
   0x555555554825 <main+91>     mov    rax, qword ptr [rbp - 0x68]
   0x555555554829 <main+95>     mov    rsi, rdx
   0x55555555482c <main+98>     mov    rdi, rax
 ► 0x55555555482f <main+101>    call   strcmp@plt <strcmp@plt>
        s1: 0x5555555549c8 ◂— 0xbed0bbd0bed0bcd0
        s2: 0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */
 
   0x555555554834 <main+106>    test   eax, eax
   0x555555554836 <main+108>    jne    main+320 <main+320>
 
   0x55555555483c <main+114>    mov    byte ptr [rbp - 0x5f], 0xe4
   0x555555554840 <main+118>    mov    byte ptr [rbp - 0x5e], 0x64
   0x555555554844 <main+122>    mov    byte ptr [rbp - 0x5d], 0xa6
─────────────────────────────────────────────────────────────────[ STACK ]─────────────────────────────────────────────────────────────────
00:0000│ rsp        0x7fffffffdf80 ◂— 0x0
01:0008│            0x7fffffffdf88 —▸ 0x5555555549c8 ◂— sar    byte ptr [rax + rdx*8 - 0x2f442f42], 1
02:0010│            0x7fffffffdf90 ◂— 0x0
03:0018│            0x7fffffffdf98 ◂— 0x0
04:0020│ rdx rsi r8 0x7fffffffdfa0 ◂— 0xf0000a /* '\n' */
05:0028│            0x7fffffffdfa8 ◂— 0xc2
06:0030│            0x7fffffffdfb0 ◂— 0x1
07:0038│            0x7fffffffdfb8 —▸ 0x55555555498d (__libc_csu_init+77) ◂— add    rbx, 1
───────────────────────────────────────────────────────────────[ BACKTRACE ]───────────────────────────────────────────────────────────────
 ► f 0   0x55555555482f main+101
   f 1   0x7ffff7e13d0a __libc_start_main+234
───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────



pwndbg> x/s 0x5555555549c8
0x5555555549c8: "молоток123\n"
pwndbg> step main
Какой пароль？
> молоток123    
верный!

флаг: wh1te%BluE$R3d
[Inferior 1 (process 10092) exited normally]
```

## Flag
флаг: wh1te%BluE$R3d

