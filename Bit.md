# Bit representation and operations

1 and 0: true or false  
8 bit = 1 byte


int index = 1;  
0000 0000 0000 0000 0000 0000 0000 0000 0001
int has 4 bytes, 32 bits, the first digit is sign bit (positive or negative), therefore, the maximum number we can represent is:  
[sign] 2^0 + 2^1 + 2^2 + ... + 2^29 + 2^30  
Totally, the limit of int is 2^31

  
源码表示法：   
"+1" 0000 0000 0000 0000 0000 0000 0000 0000 0001  
"-1" 1000 0000 0000 0000 0000 0000 0000 0000 0001  
For 0, we have both +0 and -0, not good!  
  
补码表示法(Two's complement):  
只有负数有补码  
"-1" 1000 0000 0000 0000 0000 0000 0000 0000 0001  
取反  
"-1" 1111 1111 1111 1111 1111 1111 1111 1111 1110  
加一 (-1 + 1 = 0)  
" 0" 1111 1111 1111 1111 1111 1111 1111 1111 1111  
再取反  
" 0" 0000 0000 0000 0000 0000 0000 0000 0000 0000  

int range[-2^31, 2^31 - 1] (remove 0)   
Why negative has one more value?  
"-2^31 - 1" 1111 1111 1111 1111 1111 1111 1111 1111 1111   
"-2^31"     1000 0000 0000 0000 0000 0000 0000 0000 0000  (what is?)  


