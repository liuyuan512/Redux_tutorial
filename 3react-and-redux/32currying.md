{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-3-1.mp4{% endvideo %}

下面我们看一个简单的`plate()`函数，它接收两个参数:`vegetable`和`fruit`
```
function plate(vegetables, fruit) {
  return `I ate a plate of ${vegetables} and ${fruit}!`;
}

plate('corn', 'apples');
```
现在，由于某些原因我们想要以后的某个节点再拿到fruit。其中一种实现这个需求的方式就是我们可以返回一个函数，这个函数接收一个参数fruit,再未来的，某个节点，一旦接收这个参数，这个函数就会被调用。

```
function plate(vegetables) {
  return function fruitFunc (fruit) {
    return `I ate a plate of ${vegetables} and ${fruit}!`;
  }
}

const fruitFunc = plate('corn');
```
现在我们有一个可以调用的`fruitFunc()`,给它传递一个`fruit`，此时在作用域内我们还可以访问`vegetables`(corn)。

另一种实现这种需求的没有延迟功能的方式:

```
function plate(vegetables) {
  return function fruitFunc (fruit) {
    return `I ate a plate of ${vegetables} and ${fruit}!`;
  }
}

const sentence = plate('corn')('apples');
```
当你调用plate函数时，它会返回一个`fruitFunc()`函数，并且会立马被传入‘apples’和立即执行。这个技术被用在函数式编程(同样还有Redux)里，被称作**currying**

##练习
```
function iceCreamOrder(name) {
  return function flavorPicker (flavor) {
    return function scoops (numScoops) {
      return `${name} ordered ${numScoops} scoops of ${flavor} ice cream!`;
    };
  };
}
```下面哪种调用是正确的？
![](/assets/Screen Shot 2017-09-13 at 17.03.34.png)

##Currying小结
**Currying**是一种向需要额外数据的函数提供部分参数的过程。Redux API使用currying的一部分是它的`connect()`方法。下一小节我们将介绍它。

##延伸阅读
- [Beginner’s Guide to Currying in Functional JavaScript](https://www.sitepoint.com/currying-in-functional-javascript/)
- [Gettin’ Freaky Functional w/ Curried JavaScript](https://blog.carbonfive.com/2015/01/14/gettin-freaky-functional-wcurried-javascript/)
- [Currying in JavaScript](http://kevvv.in/currying-in-javascript/)
