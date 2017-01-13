# problem
遇到的一些问题  
1......  
在使用STVD COSMIC\CXSTM8  
ulong temp32;  
uint temp16;  
temp32=temp16*10;  
编译通过，但是烧录到单片机执行，temp32的值一直不对，随机变动；  
将temp32=temp16*10；拆分成temp32=temp16；temp32*=10；编译烧录执行，一切正确。
