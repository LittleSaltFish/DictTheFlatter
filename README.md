# DictTheFlatter

## 项目简介

这是一个能够自动将多层嵌套的字典“拍扁”的小工具

## 使用场景

在使用爬虫获取到数据并开始数据清洗的时候，通常会发现从api那里获得的数据大多是一个深度嵌套的json文件。对此类文件的处理通常非常麻烦，一不小心就会搞错嵌套关系，为后续转入dataframe以及进一步分析数据带来极大困难。

使用该工具，无论是扁平化还是输出为csv格式，均可以很直观的了解到数据的大致情况。

## 实现思路

使用两个栈（在python中用list实现）分别作为输入栈和输出栈，递归调用函数，处理输入栈中仍然存在嵌套的部分。对于非嵌套的部分则弹出并放进输出栈。

为了防止不同层级的key在“拍扁时发生重名冲突，根据Json文件的特性，采用 “高层级”\_“低层级” 的格式修改命名，可以在不牺牲过多可读性的情况下，保留原有的嵌套关系。

举个栗子：

```python
# 原始字典：
{
    a:1,
    b:2,
    c:{
        d:3,
        e:4,
    }
}

# 修改后字典：
{
    a:1,
    b:2,
    c_d:3,
    c_e:4,
}
```

## 使用方法

- FlatDict(dic)  可以将字典拍扁，并返回新字典
- Flat2CSV(dic)  可以将多层嵌套字典组成的list，输出为csv

推荐使用python的json库来读取数据文件，放进list里处理
