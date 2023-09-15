# ctype.h库函数

ctype.h库函数主要包括一些字符处理函数。

<!-- toc -->

## 一、字符测试函数

### 1.isalnum函数——判断是否是英文字母或数字字符

函数原型：`int isalnum(int ch);`

isalnum函数是宏定义，不是真正的函数。
### 2.isalpha函数——判断是否为英文字母

函数原型：`int isalpha(int ch);`
### 3.isascii函数——判断ASCII码是否位于0~127

函数原型：`int isalpha(int ch);`

比如：`printf("%c%s是一个ASCII字符\n",str[i],(isascii(str[i]))?"":"不");`
### 4.iscntrl函数——判断是否为控制字符

函数原型：`int iscntrl(int ch);`

该函数的功能是判断ch是否是控制字符，即ASCII码是否位于0x00(NOL)~0x1f(VS)或等于0x7f（Delete键的ASCII码）。

```c
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
void main()
{
    int c;
    c='a';
    printf("'%c'%s\n",c,iscntrl(c)?"是控制字符":"不是控制字符");
    c=13;
    printf("ASCII码为%x的字符%s\n",c,iscntrl(c)?"是控制字符":"不是控制字符");
    c=0x7f;
    printf("ASCII码为%x的字符%s\n",c,iscntrl(c)?"是控制字符":"不是控制字符");
    system("pause");
}
```

```
'a'不是控制字符
ASCII码为d的字符是控制字符
ASCII码为7f的字符是控制字符
请按任意键继续. . .
```

### 5.isdigit函数——判断是否为数字字符

函数原型：`int isdigit(int ch);`
### 6.isgraph函数——判断是否为可打印字符（不包括空格）

函数原型：`int isgraph(int ch);`

可打印字符指可显示字符，英文字母、数字字符、标点符号都是可打印字符，可打印字符的ASCII码在33~127。换行符、回车符、空格符、Tab键对应的字符都是不可打印字符。
### 7.islower函数——判断是否为小写英文字母

函数原型：`int islower(int ch);`
### 8.isprint函数——判断是否为可打印字符（包括空格）

函数原型：`int isprint(int ch);`

```c
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
int main()
{
    int i=0;
    char str[]="Welcome to you!\nWelcome to Chungkuo!\n";
    while(isprint(str[i]))
    {
        putchar(str[i]);
        i++;
    }
    return 0;
}
```

```
Welcome to you!
Process returned 0 (0x0)   execution time : 0.054 s
Press any key to continue.
```

`\n`不可打印，所以只输出了第1个`\n`之前的字符。
### 9.ispunct函数——判断是否为标点符号

函数原型：`int ispunct(int ch);`

```c
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>
int main()
{
    char str1[]="How are you, Mr Liu!";
    char str2[]="Mobile interface development, system analyst, algorithm design!";
    int i=0,count=0;
    char *p;

    while(str1[i]!='\0')
    {
        if(ispunct(str1[i]))
            count++;
        i++;
    }
    printf("字符串%s包含%d个标点符号.\n",str1,count);
    p=str2;
    count=0;
    while(*p!='\0')
    {
        if(ispunct(*p))
            count++;
        p++;
    }
    printf("字符串%s包含%d个标点符号.\n",str2,count);
    return 0;
}
```

```
字符串How are you, Mr Liu!包含2个标点符号.
字符串Mobile interface development, system analyst, algorithm design!包含3个标点符号.
```

### 10.isspace函数——判断是否为空白字符

函数原型：`int isspace(int ch);`

C标准中空白字符有：空格（‘ ’）、换页（‘\\f’）、换行（‘\\n’）、回车（‘\\r’）、水平制表符（‘\\t’）、垂直制表符（‘\\v’）六个。

空白符|ASCII码|说明
-|-|-
''|32|空格符
'\\t'|9|水平制表符
'\\n'|10|换行
'\\v'|11|垂直制表符
'\\f'|12|换页符
'\\r'|13|回车符

### 11.isxdigit函数——判断是否是十六进制字符

函数原型：`int isxdigit(int ch);`

```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
int main()
{
    char str[3][10]={"2FE9H","3EC7","X48A"};
    int i,k,len;
    for(k=0;k<3;k++)
    {
        len=strlen(str[k]);
        for(i=0;str[i]!='\0';)
            if(isxdigit(str[k][i]))
                i++;
            else
                break;
        if(i>=len)
            printf("%s是十六进制对应的字符\n",str[k]);
        else
            printf("%s不是十六进制对应的字符\n",str[k]);
    }
    return 0;
}
```

```
2FE9H不是十六进制对应的字符
3EC7是十六进制对应的字符
X48A不是十六进制对应的字符
```

## 二、字符转换函数

### 1.tolower函数——将大写英文字母转换成小写英文字母

函数原型：`int tolower(int ch);`

该函数可以直接作为putchar函数的参数
### 2.toupper函数——将小写英文字母转换成大写英文字母

函数原型：`int toupper(int ch);`

该函数可以直接作为putchar函数的参数
### 3.toascii函数——将字符转换成ASCII码

函数原型：`int toascii(int ch);`

```c
#include <stdio.h>
#include <ctype.h>
int main()
{
    char ch;
    while(1)
    {
        printf("请输入一个字符（输入q终止程序）：");
        ch=getchar();
        if(ch=='q')
            break;
        if(ch!=10)
            printf("ASCII码为%d\n",toascii(ch));
        getchar();
    }
    return 0;
}
```

```
请输入一个字符（输入q终止程序）：g
ASCII码为103
请输入一个字符（输入q终止程序）：a
ASCII码为97
请输入一个字符（输入q终止程序）：A
ASCII码为65
请输入一个字符（输入q终止程序）：5
ASCII码为53
请输入一个字符（输入q终止程序）：U
ASCII码为85
请输入一个字符（输入q终止程序）：q

Process returned 0 (0x0)   execution time : 20.731 s
Press any key to continue.
```

