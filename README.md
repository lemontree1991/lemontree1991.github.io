# 概述

[UUID](https://link.jianshu.com/?t=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FUniversally_unique_identifier)是128位的全局唯一标识符，通常由32字节的字符串表示。它可以保证时间和空间的唯一性，也称为GUID，全称为： UUID ——[Universally Unique IDentifier](https://link.jianshu.com/?t=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FUniversally_unique_identifier)Python 中叫 UUID GUID —— Globally Unique IDentifier C# 中叫 GUID

它通过MAC地址、时间戳、命名空间、随机数、伪随机数来保证生成ID的唯一性。

UUID主要有五个算法，也就是五种方法来实现.

- Python中没有基于DCE的，所以uuid2可以忽略；
- uuid4存在概率性重复，由无映射性，最好不用；
- 若在Global的分布式计算环境下，最好用uuid1；
- 若有名字的唯一性要求，最好用uuid3或uuid5。

# 实现方法

```python
In [1]: import uuid

In [2]: uuid.uuid1()
Out[2]: UUID('c44db468-a254-11ea-9679-6014b379ef0e')

In [3]: uuid.uuid3(uuid.NAMESPACE_DNS, 'textname')
Out[3]: UUID('0d51f784-b309-386c-999a-92c2edff35d3')

In [4]: uuid.uuid4()
Out[4]: UUID('5f7847d1-f030-4d26-818e-701a3f7e7dc3')

In [5]: uuid.uuid5(uuid.NAMESPACE_DNS, 'textname')
Out[5]: UUID('f7f0ba32-929d-541b-9395-478cb51644e2')
```



## uuid1

基于时间戳 由MAC地址、当前时间戳、随机数生成。可以保证全球范围内的唯一性， 但MAC的使用同时带来安全性问题，局域网中可以使用IP来代替MAC。

## uuid2

算法与uuid1相同，不同的是把时间戳的前4位置换为POSIX的UID。不过需要注意的是python中没有基于DCE的算法，所以python的uuid模块中没有uuid2这个方法。

## uuid3(推荐)

基于名字的MD5散列值 通过计算名字和命名空间的MD5散列值得到，保证了同一命名空间中不同名字的唯一性， 和不同命名空间的唯一性，但同一命名空间的同一名字生成相同的uuid。

## uuid4

基于随机数 由伪随机数得到，有一定的重复概率，该概率可以计算出来。

## uuid5(推荐)

基于名字的SHA-1散列值 算法与uuid3相同，不同的是使用 Secure Hash Algorithm 1 

