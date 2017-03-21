# 谓词

谓词是通过NSPredicate，是通过给定的逻辑条件作为约束条件，完成对数据的筛选。

```
predicate = [NSPredicate predicateWithFormat:@"customerID == %d",n];

a = [customers filteredArrayUsingPredicate:predicate];
```