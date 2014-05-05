###Task 1
######Simple MIPS Assembly Program

```mips
   addi $s0, 44($0)         #Loads the value 44 into saved variables register 0
   addi $s1, -37($0)        #Loads the value -37 into saved variables register 1
   add $s2, $s0, $s1 #Adds the contents of saved variables registers 0 and 1 and stores the result in register 2
   sw $s2, 0x54($0)     #Stores the value contained in register 2 inside memory address x54 (hex value)
```


###Task 2
######Convert Assembly Code above to Machine Code
|  Assembly Code  | Machine Code, Binary  | Machine Code, Hex  |
|-----------------|-----------------------|--------------------|
| addi $s0, 44($0)|00100000000100000000000000101100| 0x2010002C|
|addi $s1, -37($0)|00100000000100010000000000100101| 0x2011FFDB|
|add $s2, $s0, $s1|00000010001100001001000000100000| 0x02309020|
|sw $s2, 0x54($0) |10101110010000000000000001010100| 0xAE400054|


Documentation: 29 Apr 14: C3C Bolinger explained the L36 material to me because I was gone for a doctor's appointment during class. This then led into a discussion of the objectives of CE5 Task 1; C3C Bolinger was having trouble figuring out the syntax/how to store a value, so I found the information I ended up using on this website: http://www.mrc.uidaho.edu/mrc/people/jff/digital/MIPSir.html.
