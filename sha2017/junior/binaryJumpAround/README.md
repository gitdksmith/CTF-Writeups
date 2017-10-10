# Binary - Jump Around

We start by downloading a binary called jumparound.
If we run jumparound all we get is a message saying we better jump higher. 

Lets start by opening this in gdb and looking at main.

$ gdb jumparound
(gdb) b main
(gdb) disas
   0x0000000000400626 <+0>:        push   %rbp
   0x0000000000400627 <+1>:        mov    %rsp,%rbp
   0x000000000040062a <+4>:        sub    $0x10,%rsp
   0x000000000040062e <+8>:        movl   $0x0,-0x4(%rbp)
   0x0000000000400635 <+15>:    cmpl   $0x0,-0x4(%rbp)
   0x0000000000400639 <+19>:    jne    0x400647 <main+33>
   0x000000000040063b <+21>:    mov    $0x400738,%edi
   0x0000000000400640 <+26>:    callq  0x400410 <puts@plt>
   0x0000000000400645 <+31>:    jmp    0x400651 <main+43>
   0x0000000000400647 <+33>:    mov    $0x0,%eax
   0x000000000040064c <+38>:    callq  0x400546 <print_flag>
   0x0000000000400651 <+43>:    leaveq 
   0x0000000000400652 <+44>:    retq

If we use 'ni' to move through the program one instruction at a time we see that we do not take the jne at <+19>, and when we enter the call `callq  0x400410 <puts@plt>` the function is long and convoluted. 

We also see that if we were to take that first jump at jne, we would be place right before the instruction `callq  0x400546 <print_flag>`. So lets set a break at jne.

`(gdb) b \*0x0000000000400639(edited)`

## == Flag Approach ==

I'll start of by stating that this approach did not work in the end, but it really seemed like it should have. I don't understand why it failed.

The cmpl is going to compare its argument values, which were set to be equal in the previous command. It is supposed to set the zero flag, ZF, to 1 if the values are equal. So we can set the value of ZF to 0 and force the jne to be taken.

`(gbd) set $ZF = 0`

We can do 'ni' from there but we see that the jump was not taken anyway and we failed. 

## == Change Instruction Approach ==

Since the flag approach didn't work, lets just try changing the jne opcode to a jmp opcode so we will jump no matter what.

Lets inspect the bytes at the jne instruction:

```
(gdb)  x 0x400639
0x400639 <main+19>:    0x38bf0c75
```

From looking online for x86 64 opcodes we will find that 75 is the jne opcode, and EB is the jmp opcode. Use the set command to change the instruction. Then continue the program.

```
(gdb) set (unsigned char)0x0000000000400639 = 0xeb
(gdb) x 0x400639
0x400639 <main+19>:    0x38bf0ceb
(gdb) c
Continuing.
Well done jumping, the flag is flag{f525a6abd58ce9488f3c90904149145d}
```

The end.
