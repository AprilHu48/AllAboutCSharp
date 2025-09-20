### 转载自C语言中文网

C# 程序语言提供了属性（property）成员的概念，所谓的属性就是一个机制，可以读取并写入类私有字段的值。在这个机制下，可以使用 set 设定 private 字段变量，使用 get 取得字段变量，

```
Bank A = new Bank();
A.Balance = 1000;//属性可读不可写,因此此句不成立
Console.WriteLine(A.Balance);

public class Bank
{
    private int _balance; // 默认的也是 private，所以也可以省略 private
    public int Balance // 定义 Balance 属性
    {
        get { return _balance; }
       private set { _balance = value; }//设置set为私有,该属性可读不可写
    }
}
```

可以将表达式主体(C# 6.0特性)方法应用到属性中

```
public class Bank
{
    private int _balance; // 预设也是 private，所以也可以省略 private
    public int Balance // 定义 Balance 属性 (property)
    {
        get => _balance;
        set => _balance = value;
    }
}
```

---

使用自动实操属性的概念来省略字段变量的声明，以及 get 和 set 内容。

```
public class Bank
{
    public int Balance // 定义 Balance 属性 (property)
    { get;private set; }
}
```

上述类没有成员字段，程序编译时会由编译程序自动产生私有成员字段。

也可以用表达式主体自动为属性设定初始值，

```
public class Student
{
    public int Score { get; set; } = 60;
    public string Name { get; set; } = "Hung";
}
```

在使用 set 创建属性时，也可以增加 if 条件设定,起到限制输入的作用

```
class Job
{
    private string _name;
    public string Name
    {
        get { return _name; }
        set
        {
            //Console.WriteLine(value);
            if (value.Length > 3)
                _name = value;
            else
                _name = "NA";
        }
    }
}
```

这个程序会要求 Name 属性内容必须大于 3 个字母，如果不符合规定，则定义 Name 是“NA”。