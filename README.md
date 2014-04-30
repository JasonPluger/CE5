###Task 1
######Simple MIPS Assembly Program

```
   lw $s0, 44         #Loads the value 44 into saved variables register 0
   lw $s1, -37        #Loads the value -37 into saved variables register 1
   addi $s2, $s0, $s1 #Adds the contents of saved variables registers 0 and 1 and stores the result in register 2
   sw $s2, 54($0)     #Stores the value contained in register 2 inside memory address x54 (hex value)
```

Documentation: 29 Apr 14: C3C Bolinger explained the L36 material to me because I was gone for a doctor's appointment during class. This then led into a discussion of the objectives of CE5 Task 1; C3C Bolinger was having trouble figuring out the syntax/how to store a value, so I found the information *I* ended up using on this website: http://www.mrc.uidaho.edu/mrc/people/jff/digital/MIPSir.html.
