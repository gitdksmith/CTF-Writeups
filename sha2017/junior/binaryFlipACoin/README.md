# Binary - Flip-A-Coin

The executable wants you to get 100 heads/wins to get the flag. You win by hitting enter and it randomly tells you if you got heads or tails. 


In the end I had to get a little from another writeup on this one. I was trying to 
trace through everything that was happening in the program, but there is a much simpler 
solution. 
Instead, you can guess there might be an add instruction somewhere for each time you win. 
Changing the increment value from 1 to 100 will give you the flag on your first win.

You might have to run it a couple times to get a win, but when you do it jumps you 
to 100 and you get the output bellow.

```
[*] SHA2017 Junior CTF - Flip a Coin
    Flip a coin, if it is heads you win, tails you lose!
    Win 100 times to get the flag

[*] Press enter to flip a coin

[*] It is heads! You win!

    Total wins: 100
[*] You won! Nice job! \o/
    Here is your flag:                                                                         
```

flag{d754c599d47d9b3e4a376e1d770ca8c1}

