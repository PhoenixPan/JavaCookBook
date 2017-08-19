# Bit representation and operations

## Bit representation
### Integer representation  
  int index = 1;  
  0000 0000 0000 0000 0000 0000 0000 0000 0001  
  integer has 4 bytes = 32 bits (1 byte = 8 bit)   
  The first digit is sign bit (positive or negative) so the maximum number we can represent is:   
  [sign] 2^0 + 2^1 + 2^2 + ... + 2^29 + 2^30 = 2^31     

### Ordinary binary representation 源码表示法
The leading 1 tells the number is negative  
"+1" 0000 0000 0000 0000 0000 0000 0000 0000 0001  
"-1" 1000 0000 0000 0000 0000 0000 0000 0000 0001   
However it is not good! Why? because we will have a positive zero and a negative zero!  
"+0" 0000 0000 0000 0000 0000 0000 0000 0000 0000  
"-0" 1000 0000 0000 0000 0000 0000 0000 0000 0000  


### Two's complement 补码表示法  
Positive numbers are the same as ordinary binary, only negative number has two's complement, whose value is the flip of positive number then plus one.  

For example:  
0000 0101  (binary 5)  
↓ flip  
1111 1010  (one's completement of 5)   
↓ add one  
1111 1011  (two's completement of -5)  

Another example:  
0000 0000 (0)  
↓ flip  
1111 1111 (0)  
↓ add one  
overflow, no negative 0   

### int range\[-2^31, 2^31-1\]: Why negative has one more value, -2^31?  
(1)  
0000 0001 (positive 1)  
1111 1111 (negative 1)  
(2)  
2^31-1:  0111 1111 1111 1111 1111 1111 1111 1111 1111 (the largest positive)  
-2^31+1: 1000 0000 0000 0000 0000 0000 0000 0000 0001 (corresponding largest negative)  
-2^31:   1000 0000 0000 0000 0000 0000 0000 0000 0000 (the additional negative number)  

![minimum](https://cloud.githubusercontent.com/assets/14355257/20159085/7c3d3382-a6ac-11e6-8db7-728e722cadf9.png)  

### Summary
[+1] = [00000001]原码 = [00000001]反码 = [00000001]补码  
[-1] = [10000001]原码 = [11111110]反码 = [11111111]补码  


References: 
https://www.cnblogs.com/zhangziqiu/archive/2011/03/30/ComputerCode.html  

## Bit operations
Only for integers, not float or double.  

11000011 && 10101010? 10000010 - x && x = x    
11000011 || 10101010? 11101011 - x || 0 = x  

## Left shift (<<) 
Simply move left and append 0s at right, 补零  

int | 15 | -15 
--- | --- | --- 
Original | 00001111 | 10001111
One's | 00001111 | 11110000
Two's | 00001111 | 11110001
<< 2 | 00111100 | 11000100
One's | 00111100 | 11000011
Original | 00111100 | 10111100
int | 60 | -60

## Right shift (>>)  
Move right and append sign bit at left, 算术移位的高位是补符号位

int | 15 | -15 
--- | --- | --- 
Original | 00001111 | 10001111
One's | 00001111 | 11110000
Two's | 00001111 | 11110001
>> 2 | 00000011 | 11111100
One's | 00000011 | 11111011
Original | 00000011 | 10000100
int | 3 | -4

## Unsigned right shift (>>>)  
move right and append a 0 at left, ignore sign bit, 逻辑移位的高位补0
a >>> 1  
Notice: for this operation, the bit sign will be counted towards a regular bit, which may make a negative number a positive integer  

# Question: What if I changed the sign after the shift? 
Fill the new digit with sign bit  

## How to use?  
use an integer to replace an array of booleans to represent situation:  
true true false false -> 1 1 0 0    
Three situations?   
Use two bits to represent three (more than two) situation:    
1 2 3 -> 00 01 10   

## Practice Questions
### 1.Given a number x, how to set x's k-th bit to 1?  
xxxx Kxxx  
0000 1000  
temp = temp ^ k  
```
int change(int x, int k) {
    return x | (1<<k);    
}
```
### 2.Given a number x, how to set x's k-th bit to 0?  
xxxx Kxxx  
1111 0111  (~0000 1000， invert)
temp = 2^n - 2^k  
~ 
```
int change(int x, int k) {
    return x & (~(1<<k));    
}
```
### 3. How to verify whether a number is power of two (n>=0)? 
x   = 00001000 has only one 1  
x-1 = 00000111   
return (x & (x - 1) == 0 && x != 0)

### 4. Whether letters in a word is unique?  
