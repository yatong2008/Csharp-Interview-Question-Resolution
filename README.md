# Csharp-Interview-Question-Resolution
Some explanation of Csharp interview questions 一些比较卷的Csharp（C#）面试题解析

Q-1. What will be the output of the following code snippet:
using System;
public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine(Math.Round(6.5));
            Console.WriteLine(Math.Round(11.5));
        }
    }

C#的默认Math.Round 方法不是简单的四舍五入，而是采用Banker's rounding（银行家算法），即：四舍六入五取偶

所以输出结果为
6
12