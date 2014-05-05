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

Below is the first picture I took of my testbench waveform:
![Incorrect Waveform](https://github.com/JasonPluger/CE5/blob/master/Task2_waveform.JPG?raw=true "Incorrect Waveform")


My instruction set is indeed working. I know this because during the first clock cycle, the *instr* signal contains the first instruction that I sent it in the table above (the first addi instruction), *we3* (write-enable) which controls whether or not data may be written to the register file is high thereby allowing data to be written, and the signal that contains the data to be written, *wd3* (write-data), contains X0000002c which is hex for the base 10 value 44. This value is also seen in mem location 16 while the instruction is being executed which is mem location of register $s0.  The second instruction is another *addi* and was initially wrong because I accidentally translated my instruction from binary to hex incorrectly. Because of my mistake, the *add* instruction was trying to add a value from a register that did not contain anything (and that register was therefore undefined) and *add* was therefore outputting “X” and not performing properly. Once I fixed the problem (going from instruction X20000002C to X20100002C) the second *addi* operation performed like it was supposed to; i.e. the same as the first instruction except the *aluout* signal contained the value X00000025 which is hex for the base 10 value 37. However at this point I found another mistake I had made and that was adding 37 instead of -37. So, I had to go back and alter my instructions again. This time the alterations resulted in my second *addi* instruction changing from X20118025 to X2011FFDB. Only my ‘immediate’ value changed, but it made a big difference in operation. 
The new waveform is shown below:
![Correct Waveform](https://github.com/JasonPluger/CE5/blob/master/Task2_waveform_corrected.JPG?raw=true "Correct Waveform")


After the second *addi* instruction was executed, -37 in hex appeared in mem location 17 (register $s1). The third signal is *add* and I know it performed correctly during the second iteration of my simulation because *instr* contains the hex-value that I assigned it in the testbench, *rd1* (read-data) contains the value loaded into register $s0(mem location 16) in the first *addi* instruction (44), *rd2* contains the value loaded into register $s1(mem location 17) in the second *addi* instruction(-37), *we3* is high allowing the values to be written to memory, and finally*aluout* and *wd3* both contain the sum of these values (-7) which is written to the destination register $s2(mem location 18). *sw* is the final instruction to be tested, and it operated correctly because *memwrite* is high thus allowing data to be written to memory. However *rd2* which controls what gets written to mem location 0x54 is “0” while *rd1* contains the value that I want to be written (7) which I believe is backwards; *rd2* should contain the value 7 and *rd1* shouldn’t matter.


###Task 3
######Add `ori` instruction to MIPS implementation:
Below is the new table of operations in the order they will be carried out:


|  Assembly Code  | Machine Code, Binary  | Machine Code, Hex  |
|-----------------|-----------------------|--------------------|
| addi $s0, 44($0)|00100000000100000000000000101100| 0x2010002C|
|addi $s1, -37($0)|00100000000100010000000000100101| 0x2011FFDB|
|add $s2, $s0, $s1|00000010001100001001000000100000| 0x02309020|
|ori $S3, $S2, x8000| 0 | 0 | 0 |
|sw $s2, 0x54($0) |10101110010000000000000001010100| 0xAE400054|


Below is the MIPS architechture schematic:
![Schematic](https://github.com/JasonPluger/CE5/blob/master/CE5_Schematic.jpg?raw=true "Schematic")


Below is the Decoder tables showing values that will be used for `ori` operation:
![Decoder Tables](https://github.com/JasonPluger/CE5/blob/master/CE5_DecoderValues.jpg?raw=true "Decoder Tables")


Documentation: 29 Apr 14: C3C Bolinger explained the L36 material to me because I was gone for a doctor's appointment during class. This then led into a discussion of the objectives of CE5 Task 1; C3C Bolinger was having trouble figuring out the syntax/how to store a value, so I found the information I ended up using on this website: http://www.mrc.uidaho.edu/mrc/people/jff/digital/MIPSir.html.
