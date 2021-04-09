# Briefing
> Download the file and find a way to get the flag.
> Contents: program

## Solution
Load the ElF to Ghidra



``` console
$ ./program 
I'm not going to make it that easy for you.

gdb program

pwndbg> info func
All defined functions:

Non-debugging symbols:
0x0000000000000548  _init
0x0000000000000570  puts@plt
0x0000000000000580  __stack_chk_fail@plt
0x0000000000000590  __cxa_finalize@plt
0x00000000000005a0  _start
0x00000000000005d0  deregister_tm_clones
0x0000000000000610  register_tm_clones
0x0000000000000660  __do_global_dtors_aux
0x00000000000006a0  frame_dummy
0x00000000000006aa  printFlag
0x00000000000007e3  main
0x0000000000000820  __libc_csu_init
0x0000000000000890  __libc_csu_fini
0x0000000000000894  _fini
pwndbg> disass main
Dump of assembler code for function main:
   0x00000000000007e3 <+0>:     push   rbp
   0x00000000000007e4 <+1>:     mov    rbp,rsp
   0x00000000000007e7 <+4>:     sub    rsp,0x10
   0x00000000000007eb <+8>:     mov    DWORD PTR [rbp-0x4],0x1
   0x00000000000007f2 <+15>:    cmp    DWORD PTR [rbp-0x4],0x539
   0x00000000000007f9 <+22>:    jne    0x807 <main+36>
   0x00000000000007fb <+24>:    mov    eax,DWORD PTR [rbp-0x4]
   0x00000000000007fe <+27>:    mov    edi,eax
   0x0000000000000800 <+29>:    call   0x6aa <printFlag>
   0x0000000000000805 <+34>:    jmp    0x813 <main+48>
   0x0000000000000807 <+36>:    lea    rdi,[rip+0x9a]        # 0x8a8
   0x000000000000080e <+43>:    call   0x570 <puts@plt>
   0x0000000000000813 <+48>:    mov    eax,0x0
   0x0000000000000818 <+53>:    leave  
   0x0000000000000819 <+54>:    ret    
End of assembler dump.
pwndbg> b main
Breakpoint 1 at 0x7e7
pwndbg> r
Starting program: /home/dev/Downloads/program 
ERROR: Could not find ELF base!

Breakpoint 1, 0x00005555555547e7 in main ()
LEGEND: STACK | HEAP | CODE | DATA | RWX | RODATA
────────────────────────────────────────────────────────────────────[ REGISTERS ]────────────────────────────────────────────────────────────────────
 RAX  0x5555555547e3 (main) ◂— push   rbp
 RBX  0x0
 RCX  0x7ffff7fab718 (__exit_funcs) —▸ 0x7ffff7fadb00 (initial) ◂— 0x0
 RDX  0x7fffffffe0f8 —▸ 0x7fffffffe411 ◂— 'COLORFGBG=15;0'
 RDI  0x1
 RSI  0x7fffffffe0e8 —▸ 0x7fffffffe3f5 ◂— '/home/dev/Downloads/program'
 R8   0x0
 R9   0x7ffff7fe2180 (_dl_fini) ◂— push   rbp
 R10  0x0
 R11  0xc2
 R12  0x5555555545a0 (_start) ◂— xor    ebp, ebp
 R13  0x0
 R14  0x0
 R15  0x0
 RBP  0x7fffffffdff0 —▸ 0x555555554820 (__libc_csu_init) ◂— push   r15
 RSP  0x7fffffffdff0 —▸ 0x555555554820 (__libc_csu_init) ◂— push   r15
 RIP  0x5555555547e7 (main+4) ◂— sub    rsp, 0x10
─────────────────────────────────────────────────────────────────────[ DISASM ]──────────────────────────────────────────────────────────────────────
 ► 0x5555555547e7 <main+4>             sub    rsp, 0x10
   0x5555555547eb <main+8>             mov    dword ptr [rbp - 4], 1
   0x5555555547f2 <main+15>            cmp    dword ptr [rbp - 4], 0x539
   0x5555555547f9 <main+22>            jne    main+36 <main+36>
    ↓
   0x555555554807 <main+36>            lea    rdi, [rip + 0x9a]
   0x55555555480e <main+43>            call   puts@plt <puts@plt>
 
   0x555555554813 <main+48>            mov    eax, 0
   0x555555554818 <main+53>            leave  
   0x555555554819 <main+54>            ret    
 
   0x55555555481a                      nop    word ptr [rax + rax]
   0x555555554820 <__libc_csu_init>    push   r15
──────────────────────────────────────────────────────────────────────[ STACK ]──────────────────────────────────────────────────────────────────────
00:0000│ rbp rsp 0x7fffffffdff0 —▸ 0x555555554820 (__libc_csu_init) ◂— push   r15
01:0008│         0x7fffffffdff8 —▸ 0x7ffff7e13d0a (__libc_start_main+234) ◂— mov    edi, eax
02:0010│         0x7fffffffe000 —▸ 0x7fffffffe0e8 —▸ 0x7fffffffe3f5 ◂— '/home/dev/Downloads/program'
03:0018│         0x7fffffffe008 ◂— 0x100000000
04:0020│         0x7fffffffe010 —▸ 0x5555555547e3 (main) ◂— push   rbp
05:0028│         0x7fffffffe018 —▸ 0x7ffff7e137cf (init_cacheinfo+287) ◂— mov    rbp, rax
06:0030│         0x7fffffffe020 ◂— 0x0
07:0038│         0x7fffffffe028 ◂— 0x5aab592ba0011aac
────────────────────────────────────────────────────────────────────[ BACKTRACE ]────────────────────────────────────────────────────────────────────
 ► f 0   0x5555555547e7 main+4
   f 1   0x7ffff7e13d0a __libc_start_main+234
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
pwndbg> p printFlag()
'printFlag' has unknown return type; cast the call to its declared return type
pwndbg> p (void)printFlag()
$1 = void
pwndbg> p (void)printFlag(5a0)
Invalid number "5a0".
pwndbg> p (void)printFlag(0x5a0)
$2 = void
pwndbg> p (void)printFlag(0x539)
Flag: patchItFixIt
$3 = void
```

## Flag
Flag: patchItFixIt
