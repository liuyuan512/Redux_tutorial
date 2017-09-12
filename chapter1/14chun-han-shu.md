{% video %}https://s3.cn-north-1.amazonaws.com.cn/u-vid-hd/fRCI1Z51dII.mp4{% endvideo %}

##什么是纯函数
纯函数是Redux应用程序中的状态更新的组成部分。纯函数的定义:
1. 只要传递相同的参数，一定返回相同的结果
2. 返回的结果只依赖于传递给他们的参数
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
`calculateTip()`计算并且返回一个数值。然而这个数值依赖于函数之外的变量`tipPercentage`。 由于它不满足纯函数的第二个条件:返回的结果只依赖于传递给他们的参数. 因此它不是纯函数。 我们可以通过把这个函数之外的变量，当做函数的第二个参数来传递，就会把它转换成纯函数:
```
const calculateTip = (cost, tipPercentage = 0.15) => cost * tipPercentage;

```

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-5-2.mp4{% endvideo %}

##无副作用

纯函数的其中一个条件就是不产生副作用。副作用是指函数与它以外的世界进行的交互，包括：
- 做一个HTTP请求
- 修改外部state
- 检索现在的日期
- `Math.random()`
- 在console里打印消息
- 添加数据库

##练习
![](/assets/Screen Shot 2017-09-12 at 14.20.28.png)

![](/assets/Screen Shot 2017-09-12 at 14.20.52.png)

##使用纯函数

纯函数是[函数式编程](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)的核心元素。 除了可以避免数据修改和产生副作用，纯函数很好的引领了组件的概念.

首先，纯函数是固定的模块，这样易于测试。由于只要给定同样的参数，纯函数就会返回同样的结果，你就不需要担心应用的其它部分会影响输出数据。在调试和检查的时候，这些特点就提供了很大的方便。

除此之外，纯函数使得维护代码变得非常简单。纯函数的特点之一是不产生任何的副作用，这也就是说，假如你重构代码，修改纯函数并不会对这个函数外面的世界产生影响。

尽管在一个应用里使用纯函数会产生很多益处，你还是可以在你的应用里使用纯函数或者非纯函数。使用非纯函数并不是"坏的编程",例如一个利用event handler更新DOM的按钮，就不适合用纯函数，因为event handler更新的DOM（产生了副作用）。

纯函数可以提供更好的代码质量，在构建应用程序时考虑这一点，会有助于你变得更优秀。

##小结

纯函数并非Redux(甚至JavaScript)所特有的，但是他们都在应用里提供了可预测性。下一小节我们会学习一下被称作**reducers**的纯函数，它会返回一个新的state。Reducers是基于Array的`reduce()`方法，我们先来看一下它！

##延伸阅读

- [什么是纯函数？](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)
- [什么是函数式编程？](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)
- [The Case for Purity](https://drboolean.gitbooks.io/mostly-adequate-guide/ch3.html#the-case-for-purity)

