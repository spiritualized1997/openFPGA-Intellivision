# openFPGA-Intellivision
Intellivision core for openFPGA on Analogue Pocket
-

Enjoy Intellivision games with this core.  The Intellivoice is fully supported.

All Intellivision files (games and the EXEC) must be in the .intv format. 
Separate .H and .L files, and other formats are not supported.

To use this core, you need to place exec.intv into  
/Assets/intv/Spiritualized.Intv/exec.intv

For the Intellivoice, you need to place the 2048 byte 012.BIN file into  
/Assets/intv/Spiritualized.Intv/012.BIN

Button mapping uses "chording".  L and R triggers are used to input the various numeric
inputs:

L trigger + up = 0  
L trigger + up + right = 1  
L trigger + right = 2  
L trigger + right + down = 3  
L trigger + down = 4  
L trigger + down + left = 5  
L trigger + left = 6  
L trigger + left + up = 7  

R trigger + up = 8  
R trigger + right = 9  

B = L2 button  
Y = R2 button  
X/A = L1+R1 buttons (they are wired together on the intv controller)  

start = enter  
select = clear  

.intv file format:

This is a block format and is pretty simple.  Each block contains the start address
where the data lives in intv space, and then how many words to load.

size  type    description  
-------------------------  
(data block)  
4 int32 start address  
4 int32 length  
2*n int16 data to load  
(last block)  
4 int32 0x00000000  
4 int32 0x00000000  
EOF  

The address is the intv WORD address, and not a byte address.  The length is likewise
in words, and not bytes.

The load address and the length must both
be a multiple of 2.  i.e. a load address of 0x1001 is not allowed.  Addresses of 0x1000
and 0x1002 are allowed, however.  Likewise, the length should be a multiple of 2 also.
