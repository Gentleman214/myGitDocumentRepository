## javascript
***
#### 1.循环语句
##### 1.1 break和continue的区别
break跳出循环，continue终止本轮循环，返回循环结构头部，开始下一轮循环
***
##### 1.2 label
标签，相当于定位符。
- 跳出多重循环：
```js
top:
  for() {
    for() {
      for() {
        break top // 标签(top)时，只能跳出内层循环，加上label可以跳出多重循环
      }
    }
  }
```
- 跳出代码块
***

#### 2.数据类型
number, string, boolean, null, undefine, object
##### 2.1 if(x),当x为以下6种数据类型时，x为false，否则为true
null, undefine, false, 0, NaN, 空字符串
注意，if({}) 和 if([]) 都是true
***
##### 2.2 Infinity(无穷)
##### 2.3 与数值相关的方法
(1)parseInt 将字符串转为整数，如果不是字符串，会先转换为字符串。
一个字符一个字符的转，遇到不能转换的就终止，所以`parseInt('13e5')`结果是13而不是135
(2)


