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

int range[-2^31, 2^31-1] (remove 0)   
Why negative has one more value?  
"-2^31-1" 1111 1111 1111 1111 1111 1111 1111 1111 1111   
"-2^31"   1000 0000 0000 0000 0000 0000 0000 0000 0000  (what is?)  


11000011 && 10101010? 10000010: only 1 && 1 = 1  
11000011 || 10101010? 11101011:      x || 0 = x  

## Left shift
int a = 10000001
a = a * 2
move left and append a 0 at right, don't worry about sign digit
a << 1  00000010

## Right shift >>
int a = 011100101
a = a / 2
move right and append a 0 at left, sign bit would be the same as before
a >> 1  001110010
a >> 2  000111001

## Unsigned right shift >>>
move right and append a 0 at left, ignore sign bit
a >>> 1

## How to use?  
use an integer to replace an array of booleans to represent situation:  
true true false false -> 1 1 0 0    
Three situations?   
Use two bits to represent three (more than two) situation:    
1 2 3 -> 00 01 10   

##### 1.Given a number x, how to set x's k-th bit to 1?  
xxxx Kxxx  
0000 1000  
temp = temp ^ k  
```
int change(int x, int k) {
    return x | (1<<k);    
}
```
##### 2.Given a number x, how to set x's k-th bit to 0?  
xxxx Kxxx  
1111 0111  (~0000 1000， invert)
temp = 2^n - 2^k  
~ 
```
int change(int x, int k) {
    return x & (~(1<<k));    
}
```
##### 3. How to verify whether a number is power of two (n>=0)? 
x   = 00001000 has only one 1  
x-1 = 00000111   
return (x & (x - 1) == 0 && x != 0)
