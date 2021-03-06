{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-6-1.mp4{% endvideo %}

#Array的reduce()方法
`.reduce()`的核心思想就是它接受很多的数值作为参数，但是返回的确实一个单一的值。`.reduce()`是一个高阶函数，就是说它接受一个函数作为参数。

>##!高阶函数!
>`.map()`和`.filter()`方法同样也是高阶函数，它们接受一个函数作为它们的第一个参数。

下面看一下`.reduce()`函数的强大之处，下面有个`iceCreamStats`数组，显示了每一个队员吃了多少冰淇淋。
```

const iceCreamStats = [
  {
    name: 'Amanda',
    gallonsEaten: 3.8
  },
  {
    name: 'Geoff',
    gallonsEaten: 5.2
  },
  {
    name: 'Tyler',
    gallonsEaten: 1.9
  },
  {
    name: 'Richard',
    gallonsEaten: 7923
  }
];
```
如果我们想要得到这个小队一共吃了多少的冰淇淋，那么我们就得自己算一下了，但是这显然不是我们应该做的事情。我们可以将这个数据**reduce**成一个单一的数字--这其实就是`.reducer`方法做的事情！下面看一下怎么使用这个方法

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-6-2.mp4{% endvideo %}

这里是我们刚刚使用的`.reduce()`代码:
```
iceCreamStats.reduce( (accumulator, currentValue) => {
  return accumulator + currentValue.gallonsEaten;
}, 0);
```
![](/assets/31cc5290-a186-4408-bbfe-bf929f981d13)


##小结
`.reduce()`是一个强大的方法，它可以使你将一个庞大的数据reduce成一个单一的值。Redux同样是利用了这个原则，使用`reducers`来更新它的数据store。下面的教程里会仔细讲解！

- [Array.prototype.reduce on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce?v=b)