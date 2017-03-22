# 常用调试命令

    * po: 打印对象, 调用对象的description方法, 是print-object 的简写
    
    * expr: 可以在调试时动态执行指定表达式, 并将结果打印出来, 很有用的命令
    
    *print: 也是打印命令, 需要指定类型
    
    * bt: 打印调用堆栈, 是thread backtrace 的简写, 加 all 可以答应所有thread 的堆栈
    
    * br l: 是breakpoint list 的简写
    
# BAD_ACCESS 在什么情况下出现?

    * 访问一个僵尸对象, 访问僵尸对象的成员变量或者向其发送消息
    
    * 死循环
    
# 如果调试 BAD_ACCESS 错误

    * 设置全局端点快速定位问题代码所在行
    
    * 开启僵尸对象调试功能
    
    
    
    
    
    
<br />
<br />
<br />
