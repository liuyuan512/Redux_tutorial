{% video %}https://s3.cn-north-1.amazonaws.com.cn/u-vid-hd/fRCI1Z51dII.mp4{% endvideo %}

#什么是纯函数
纯函数是Redux应用程序中的状态更新的组成部分。纯函数的定义:
1. 只要传递相同的参数，一定返回相同的结果
2. 完全依赖于传递给他们的参数
3. 不会产生副作用
我们看一个纯函数，square():
```
//`square()`是一个纯函数
const square = x> x*x;
```
`square()`是一个纯函数,因为只要给它一样的参数，它总是会输出同样的结果。这个结果不依赖与任何其它的值，并且只有结果的值被返回，不会产生任何副作用。

下面再看一个非纯函数的列子:`calculateTip()`
```
//`calculateTip()`不是纯函数

const tipPercentage = 0.15;

const calculateTip = cost => cost * tipPercentage;
```