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

Q-2. What will be the output of the following code snippet:
using System;
public class Program
    {
        public static void Main(string[] args)
        {
            int[] i = new int[0];
            Console.WriteLine(i[0]);
        }
    }

new int[0] 将会建立一个新的空的数组对象，没有元素，i[0]将会尝试访问第一个元素，超出访问范围，打印IndexOutOfRangeException

Q-3. What will be the output of the following code snippet:
using System;
public class Program
    {
        public static void Main(string[] args)
        {
            byte num = 100;
            dynamic val = num;
            Console.WriteLine(val.GetType());
            val += 100;
            Console.WriteLine(val.GetType());
        }
    }
dynamic是FrameWork4.0的新特性。dynamic的出现让C#具有了弱语言类型的特性。编译器在编译的时候不再对类型进行检查，编译期默认dynamic对象支持你想要的任何特性。
dynamic vs var
var和dynamic完全是两个概念，根本不应该放在一起做比较。var实际上是编译期抛给我们的“语法糖”，一旦被编译，编译期会自动匹配var 变量的实际类型，并用实际类型来替换该变量的申明，这看上去就好像我们在编码的时候是用实际类型进行申明的。而dynamic被编译后，实际是一个object类型，只不过编译器会对dynamic类型进行特殊处理，让它在编译期间不进行任何的类型检查，而是将类型检查放到了运行期。

所以第一行输出为System.Byte
第二行的+=操作将类型转换成了 System.Int32??????

Q-4. What will be the output of the following code snippet:
using System;
public class Program
    {
        public static void Main(string[] args)
        {
            #if (!pi)
                Console.WriteLine("i");
            #else 
                Console.WriteLine("PI undefined");
            #endif
                Console.WriteLine("ok");
                Console.ReadLine();
        }
    }
C# 预处理器指令
条件编译
使用四个预处理器指令来控制条件编译：

#if：打开条件编译，其中仅在定义了指定的符号时才会编译代码。
#elif：关闭前面的条件编译，并基于是否定义了指定的符号打开一个新的条件编译。
#else：关闭前面的条件编译，如果没有定义前面指定的符号，打开一个新的条件编译。
#endif：关闭前面的条件编译。
如果 C# 编译器遇到 #if 指令，最后跟着一个 #endif 指令，则仅当定义指定的符号时，它才编译这些指令之间的代码。 与 C 和 C++ 不同，不能将数字值分配给符号。 C# 中的 #if 语句是布尔值，且仅测试是否已定义该符号。 例如：

因为没有这一句#define PI，所以#if (!pi) 成立？

Q-49. What will be the output of the following code snippet:
using System;
public class Program
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("H" + 'I');
            Console.WriteLine('h' + 'i');
        }
    }

根据文档 (http://msdn.microsoft.com/en-us/library/x9h8tsay%28v=vs.110%29.aspx) 字符串 char 类型可以被隐性转化成整型， 字符串也没有定义操作符 +， 所以第二行打印209
HI
209