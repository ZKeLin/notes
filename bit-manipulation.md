### 基本的字节运算
##### 设置某一位为1
```
function set_bit(x,position){
 let mask = 1 << postion;
 return x | mask;
}
```
##### 清除某一位（即设置某一位为0）
```
function clear_bit(x,position){
 let mask = 1 << postion;
 return x & ~mask;
}
```
##### 反转某一位
```
function flip_bit(x,position){
 let mask = 1 << postion;
 return x ^ mask;
}
```
##### 判断某一位是否为1
```
function is_bit_set(x,position){
 let shifted = x >> postion;
 return shited & 1;
}
```
##### 修改某一位置的值
```
function modify_bit(x,position,state){
 let mask = 1 << postion;
 return (x & ~mask) | (-state & mask); //-state 表示state取反加一即补码
}
```
##### 判断是否是偶数
```
function is_even(x){
 return (x & 1) == 0;
}
```
##### 判断是否是2的次幂
```
function is_power_of_two(x){
 return (x & x-1) == 0;
}
```
###### ["来自于这"](https://www.youtube.com/watch?v=7jkIUgLC29I )