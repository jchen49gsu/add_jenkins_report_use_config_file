
# add_jenkins_report_use_config_file
## Config file

### desire format in jenkin_reg.cfg
```python
[section]
[[subsection]]
KEY1=['value1','value2']
KEY2=[]
KEY3='\sCPU\s=\s(\S+)\saverage_cycle\s=\s(\S+)\saverage_bw\s=\s(\S+)\siops\s=\s(\S+)\s.*'
```
### read
```python
import ConfigParser
conf = ConfigParser.ConfigParser()
conf.read("jenkins_reg.cfg")
```
by default it will convert the character read from the config file to be lower case. For case sensitive, use this
```python
conf.optionxform = str
```
### section and subsection
```python
sec = conf.sections()
print sec
>>> ['section', '[subsection']

key1= sec[0]
key2 = sec[1][1:] #need to start from index 1
print key1, key2
>>> section subsection
```
### items (return a list)
```python
ITEMS1 =conf.items("section")
ITEMS2 =conf.items("[subsection")
print ITEMS1
print ITEMS2

>>>
[]
[('key1', "['value1','value2']"), ('key2', '[]'), ('key3', "'\\sCPU\\s=\\s(\\S+)\\saverage_cycle\\s=\\s(\\S+)\\saverage_bw\\s=\\s(\\S+)\\siops\\s=\\s(\\S+)\\s.*'")]

```
### nested keys and nested values in items
```python
nested_keys = []
nested_values=[]
for item in ITEMS2:
	nested_keys.append(item[0])
	nested_values.append(item[1])
print nested_keys
print "nested_values is:", nested_values
>>> 
['key1', 'key2', 'key3']
nested_values is: ["['value1','value2']", '[]', "'\\sCPU\\s=\\s(\\S+)\\saverage_cycle\\s=\\s(\\S+)\\saverage_bw\\s=\\s(\\S+)\\siops\\s=\\s(\\S+)\\s.*'"]
```
nested_values are string
```python
print nested_values[0]
print type(nested_values[0])
>>> 
['value1','value2']
<type 'str'>
```
******if need to change to be list for the nested_values, use this
```python
nested_value_value = list(ast.literal_eval(conf.get("[subsection",nested_keys[0])))
print nested_value_value
print type(nested_value_value)
>>> 
['value1', 'value2']
<type 'list'>
```

*****if need to change the list to be string, use this
```python
nested_value_value = list(ast.literal_eval(conf.get("[subsection",nested_keys[2])))
print nested_value_value
>>>
['\\', 's', 'C', 'P', 'U', '\\', 's', '=', '\\', 's', '(', '\\', 'S', '+', ')', '\\', 's', 'a', 'v', 'e', 'r', 'a', 'g', 'e', '_', 'c', 'y', 'c', 'l', 'e', '\\', 's', '=', '\\', 's', '(', '\\', 'S', '+', ')', '\\', 's', 'a', 'v', 'e', 'r', 'a', 'g', 'e', '_', 'b', 'w', '\\', 's', '=', '\\', 's', '(', '\\', 'S', '+', ')', '\\', 's', 'i', 'o', 'p', 's', '\\', 's', '=', '\\', 's', '(', '\\', 'S', '+', ')', '\\', 's', '.', '*']

nested_value_value=''.join(map(str,nested_value_value))
print nested_value_value

>>>
\sCPU\s=\s(\S+)\saverage_cycle\s=\s(\S+)\saverage_bw\s=\s(\S+)\siops\s=\s(\S+)\s.*

```
**********Create nested dictionary
```python
dic ={}
nested_values_dic = {}
nested_values_dic["nested_key"] = "nested_value"
dic["key"]=nested_values_dic
print dic
```
### write




### enumerate()使用
如果对一个列表，既要遍历索引又要遍历元素时，首先可以这样写：
```python
list1 = ["这", "是", "一个", "测试"]
for i in range (len(list1)):
    print i ,list1[i]1
2
3
```
上述方法有些累赘，利用enumerate()会更加直接和优美：
```python
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

```
```python
•enumerate还可以接收第二个参数，用于指定索引起始值，如：
list1 = ["这", "是", "一个", "测试"]
for index, item in enumerate(list1, 1):
    print index, item
>>>
1 这
2 是
3 一个
4 测试
```
### regular expression
```python
import re
text = "good is not bad, but cool"
regex=re.compile(r'\w*oo\w*')
print regex.findall(text) #查找所有包含'oo'的单词
```
link to test re
https://regex101.com/

```python
\sCPU\s=\s(\S+)\saverage_cycle\s=\s(\S+)\saverage_bw\s=\s(\S+)\siops\s=\s(\S+)\s.*
\s matches any whitespace character (equal to [\r\n\t\f\v ])

```

## PDB

Two way to do the debug with terminal:
1. use python file.py and set break point
2. use python -m pdb file.py and in the file.py import pdb and pdb.set_trace()




https://www.cnblogs.com/jiayongji/p/7469214.html


