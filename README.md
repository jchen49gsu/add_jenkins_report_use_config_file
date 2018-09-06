# add_jenkins_report_use_config_file
enumerate()使用
•如果对一个列表，既要遍历索引又要遍历元素时，首先可以这样写：
<pre>
list1 = ["这", "是", "一个", "测试"]
for i in range (len(list1)):
    print i ,list1[i]1
2
3
</pre>
•上述方法有些累赘，利用enumerate()会更加直接和优美：
<pre>
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1):
    print index, item
>>>
0 这
1 是
2 一个
3 测试1
2
3
4
5
6
7
8

</pre>
<pre>
•enumerate还可以接收第二个参数，用于指定索引起始值，如：
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1, 1):
    print index, item
>>>
1 这
2 是
3 一个
4 测试
</pre>


# Config file

## desire format

## read
```python
import ConfigParser
conf = ConfigParser.ConfigParser()
conf.read("jenkins_reg.cfg")
```
### section
```python
sec = conf.sections()
```

## write
## subsection












