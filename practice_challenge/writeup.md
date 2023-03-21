okay so first thing i did was open up the file in ida as well, to get a feel of how the control flow was (through the flow charts)

looking at the pseudocode felt useless, so i continued looking at the graph of main and what i noticed was that there was a condiional loop, which checked the value of rsi and 47 

then looking a little up, i saw rsi being used to increment the address value inside rbx and compare that with al

looking inside the al reg, i saw that ascii values were being stored, letter by letter
so there was a char by char comparison of what you input vs an already stored answer

aight so, all i have to do is find out the value at each checkpoint for al, and store those somewhere
but where in memory is the checking happening?

spent about 2 hours trying to compare the flow execution with gdb and ida side by side and got nowhere 
then got the hint about rebasing in gdb

turns out rebasing changes the base address of the program, as in where it loads in memory, not where the execution begins
i noticed that in this program, the start function was loading 4417 ints after whatever i set as the base address
so quickly subtracted hex(4417) from my entry point (from gdb) and set that as the base instead - worked perfectly 

now using the help of ida, i jumped into the main function in gdb and found exactly what i needed
set relevant breakpoints, printed the values on the terminal 

i saved the output in a file, and used a little python to format it how i wanted it and saved it in a list and converted those to chars
boom flag

```
lactf{m4yb3_th3r3_1s_s0m3_m3r1t_t0_us1ng_4_db}
```

