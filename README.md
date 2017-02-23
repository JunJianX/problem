# problem
遇到的一些问题  
1......  
在使用STVD COSMIC\CXSTM8  
ulong temp32;  
uint temp16;  
temp32=temp16×10;  
编译通过，但是烧录到单片机执行，temp32的值一直不对，随机变动；  
将temp32=temp16×10；拆分成temp32=temp16；temp32×=10；编译烧录执行，一切正确。  

2......  
unsigned char bw;
bw=bw+2;
bw=bw>>1;

上面两句在STVP+COSMIC 中编译都会出现”truncating assignment“ 警告
要怎样改才不会出现 ”truncating assignment“ 警告
也就是  使用这类语句都会   如  变量=变量+常数    变量=变量-常数   变量=变量\*常数    变量=变量/常数 
都会出现 “truncating assignment”警告 
|---------------------------------------------------------------------------------------|
终于搞明白，多谢楼下的几位淫兄 ，散分结贴了；
上面在使用8位变量操作前，都应该强制声明变量为8 位才不会出现警告，看了些资料得知是因STVD编译器默认是16位变量。或许这是C语言的标准

上面改为下面后语句编译全通过，由于我是刚接触STM8，有点菜了，希望大家多指点
unsigned char bw;
bw=（unsigned char ) ( bw+2）;
bw=( unsigned char ) ( bw>>1 );

就连函数参数是8位的变量，都应这样增加类型强制
write24c02 ( 0x00 ,  ( unsigned char  )  ( bw+1 )  );

格式为：( unsigned char )（表达式）;如是16位的变量则不需要这样声明， 
