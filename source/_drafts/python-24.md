---
title: python24点计算器
tags:
  - Python
  - 编程
id: 661
categories:
  - 代码
date: 2017-09-03 20:56:00
---

最近在玩[@林木木](http://www.imuum.com/)大神的[决战24点](https://pk24go.cn/)。规则很简单，给出四个数（0~13）用加减乘除四则运算算成24，每个数只能用一次，先算出结果为胜。
用代码解决这个问题，我的思路很简单，就是穷举，把所有的算法列出来，然后代数进去算。。但写起来真TM要命，加减乘除四个排列，
[![](http://ffshine.xyz/blog/wp-content/uploads/2017/09/point_24_python.png)](http://ffshine.xyz/blog/wp-content/uploads/2017/09/point_24_python.png)
还要考虑括号问题，零不能做除数...。写出来的代码让人犯密恐。我脑袋从来没有这么乱过。到现在为止，我也没有能够把所有的算法列出来。


<storng>代码如下</storng>
```python
    def point_24(a,b,c,d):
        if(a+b+c+d == 24):return(str(a)+'+'+str(b)+'+'+str(c)+'+'+str(d))
        elif(a+b+c-d == 24):return(str(a)+'+'+str(b)+'+'+str(c)+'-'+str(d))
        elif(a+b-c-d == 24):return(str(a)+'+'+str(b)+'-'+str(c)+'-'+str(d))
        elif(a-b-c-d == 24):return(str(a)+'-'+str(b)+'-'+str(c)+'-'+str(d))
        elif(a*b*c*d == 24):return(str(a)+'*'+str(b)+'*'+str(c)+'*'+str(d))
        elif(a*b*c/d == 24):return(str(a)+'*'+str(b)+'*'+str(c)+'/'+str(d))
        elif(a*b/c/d == 24):return(str(a)+'*'+str(b)+'/'+str(c)+'/'+str(d))
        elif(a/b/c/d == 24):return(str(a)+'/'+str(b)+'/'+str(c)+'/'+str(d))

        #++*
        elif(a+b+(c*d) == 24):return(str(a)+'+'+str(b)+'+('+str(c)+'*'+str(d)+')')
        elif(a+(b+c)*d == 24):return(str(a)+'+('+str(b)+'+'+str(c)+')*'+str(d))
        elif((a+b+c)*d == 24):return('('+str(a)+'+'+str(b)+'+'+str(c)+')*'+str(d))
        elif ((a+b)*(d+c) == 24):return('('+str(a)+'+'+str(b)+')*('+str(d)+'+'+str(c)+')')

        #++/
        elif(a+b+(c/d) == 24):return(str(a)+'+'+str(b)+'+('+str(c)+'/'+str(d)+')')
        elif(a+(b+c)/d == 24):return(str(a)+'+('+str(b)+'+'+str(c)+')/'+str(d))
        elif((a+b+c)/d == 24):return('('+str(a)+'+'+str(b)+'+'+str(c)+')/'+str(d))
        elif ((a + b) / (d + c) == 24):return('('+str(a)+'+'+str(b)+')/('+str(d)+'+'+str(c)+')')

        #+-*
        elif(a+b-(c*d) == 24):return(str(a)+'+'+str(b)+'-('+str(c)+'*'+str(d)+')')
        elif(a+(b-c)*d == 24):return(str(a)+'+('+str(b)+'-'+str(c)+')*'+str(d))
        elif((a+b-c)*d == 24):return('('+str(a)+'+'+str(b)+'-'+str(c)+')*'+str(d))
        elif(a-b+(c*d) == 24):return(str(a)+'-'+str(b)+'+('+str(c)+'*'+str(d)+')')
        elif(a-(b+c)*d == 24):return(str(a)+'-('+str(b)+'+'+str(c)+')*'+str(d))
        elif((a+b)*c-d == 24):return('('+str(a)+'+'+str(b)+')*'+str(c)+'-'+str(d))

        #+-/
        elif(a+b-(c/d) == 24):return(str(a)+'+'+str(b)+'-('+str(c)+'/'+str(d)+")")
        elif(a+(b-c)/d == 24):return(str(a)+'+('+str(b)+'-'+str(c)+')/'+str(d))
        elif((a+b-c)/d == 24):return("("+str(a)+'+'+str(b)+'-'+str(c)+')/'+str(d))
        elif(a-b+(c/d) == 24):return(str(a)+'-'+str(b)+'+('+str(c)+'/'+str(d)+")")
        elif(a-(b+c)/d == 24):return(str(a)+'-('+str(b)+'+'+str(c)+')/'+str(d))
        elif ((a + b) /c -d == 24):return("("+str(a)+'+'+str(b)+')/'+str(c)+'-'+str(d))

        #--*
        elif(a-b-(c*d) == 24):return(str(a)+'-'+str(b)+'-('+str(c)+'*'+str(d)+')')
        elif(a-(b-c)*d == 24):return(str(a)+'-('+str(b)+'-'+str(c)+')*'+str(d))
        elif((a-b-c)*d == 24):return("("+str(a)+'-'+str(b)+'-'+str(c)+')*'+str(d))
        elif((a-b)*c-d == 24):return("("+str(a)+'-'+str(b)+')*'+str(c)+'-'+str(d))

        #--/
        elif(a-b-(c/d) == 24):return(str(a)+'-'+str(b)+'-('+str(c)+'/'+str(d)+")")
        elif(a-(b-c)/d == 24):return(str(a)+'-('+str(b)+'-'+str(c)+')/'+str(d))
        elif((a-b-c)/d == 24):return("("+str(a)+'-'+str(b)+'-'+str(c)+')/'+str(d))
        elif ((a - b) / c - d == 24):return ("("+str(a)+'-'+str(b)+')/'+str(c)+'-'+str(d))

        #+**
        elif(a+(b*c*d) == 24):return(str(a)+'+('+str(b)+'*'+str(c)+'*'+str(d)+")")
        elif((a+b)*c*d == 24):return("("+str(a)+'+'+str(b)+')*'+str(c)+'*'+str(d))
        elif((a*b)+(c*d) == 24):return("("+str(a)+'*'+str(b)+')+('+str(c)+'*'+str(d)+")")
        elif((a+b*c)*d == 24):return("("+str(a)+'+'+str(b)+'*'+str(c)+')*'+str(d))

        #+*/
        elif(a+(b/c*d) == 24):return(str(a)+'+('+str(b)+'/'+str(c)+'*'+str(d)+")")
        elif((a+b)/c*d == 24):return ("("+str(a)+'+'+str(b)+')/'+str(c)+'*'+str(d))
        elif((a*b)+(c/d) == 24):return("("+str(a)+'*'+str(b)+')+('+str(c)+'/'+str(d)+")")
        elif((a+b/c)*d == 24):return("("+str(a)+'+'+str(b)+'/'+str(c)+')*'+str(d))

        #+//
        elif(a+(b/c/d) == 24):return(str(a)+'+('+str(b)+'/'+str(c)+'/'+str(d)+")")
        elif((a+b)/c/d == 24):return("("+str(a)+'+'+str(b)+')/'+str(c)+'/'+str(d))
        elif((a/b)+(c/d) == 24):return("("+str(a)+'/'+str(b)+')+('+str(c)+'/'+str(d)+')')
        elif((a+b/c)/d == 24):return("("+str(a)+'+'+str(b)+'/'+str(c)+')/'+str(d))

        #-//
        elif(a-(b/c/d) == 24):return(str(a)+'-('+str(b)+'/'+str(c)+'/'+str(d)+')')
        elif((a-b)/c/d == 24):return("("+str(a)+'-'+str(b)+')/'+str(c)+'/'+str(d))
        elif((a/b)-(c/d) == 24):return("("+str(a)+'/'+str(b)+')-('+str(c)+'/'+str(d)+")")
        elif ((a -b / c) / d == 24):return("("+str(a)+'-'+str(b)+'/'+str(c)+')/'+str(d))

        #-/*
        elif(a-(b/c*d) == 24):return(str(a)+'-('+str(b)+'/'+str(c)+'*'+str(d)+")")
        elif((a-b)/c*d == 24):return("("+str(a)+'-'+str(b)+')/'+str(c)+'*'+str(d))
        elif((a*b)-(c/d) == 24):return("("+str(a)+'*'+str(b)+')-('+str(c)+'/'+str(d)+")")
        elif ((a - b / c) * d == 24):return("("+str(a)+'-'+str(b)+'/'+str(c)+')*'+str(d))
        #除数不能为0
        elif((a-b) != 0):
            if(c/(a-b)*d == 24):return(str(c)+"/("+str(a)+"-"+str(b)+")*"+str(d))
            else:
                return 0

        #-**
        elif(a-(b*c*d) == 24):return(str(a)+'-('+str(b)+'*'+str(c)+'*'+str(d)+')')
        elif((a-b)*c*d == 24):return('('+str(a)+'-'+str(b)+')*'+str(c)+'*'+str(d))
        elif((a*b)-(c*d) == 24):return('('+str(a)+'*'+str(b)+')-('+str(c)+'*'+str(d)+')')
        elif ((a - b * c) * d == 24):return('('+str(a)+'-'+str(b)+'*'+str(c)+')*'+str(d))
        elif (((a * b) - c) * d == 24):return ('((' + str(a) + '*' + str(b) + ')-' + str(c) + ')*' + str(d))
        else:return(0)

    def main():
        a = int(input("A:"))
        b = int(input("B:"))
        c = int(input("C:"))
        d = int(input("D:"))

        lis=[
        point_24(a,b,c,d),
        point_24(a,b,d,c),
        point_24(a,c,d,b),
        point_24(a,c,b,d),
        point_24(a,d,b,c),
        point_24(a,d,c,b),
        point_24(b,a,c,d),
        point_24(b,a,d,c),
        point_24(b,c,a,d),
        point_24(b,c,d,a),
        point_24(b,d,c,a),
        point_24(b,d,a,c),
        point_24(c,a,b,d),
        point_24(c,a,d,b),
        point_24(c,b,d,a),
        point_24(c,b,a,d),
        point_24(c,d,a,b),
        point_24(c,d,b,a),
        point_24(d,a,b,c),
        point_24(d,a,c,b),
        point_24(d,b,c,a),
        point_24(d,b,a,c),
        point_24(d,c,a,b),
        point_24(d,c,b,a),
                ]

        #去重
        lis =list(set(lis))

        for i in lis:
            if(i !=0 ):
                print(i)
    while(True):
        try:
            main()
        except:
            exit()
```

代码还有很多缺点*   算法不完全，特别是带括号的，双重括号的情况基本没有考虑。
*   虽然有简单的去重操作，但还是不能判断出位置不同，但实际相同的情况
*   最后没有一个好的结束循环的方法，只能靠错误调用exit()