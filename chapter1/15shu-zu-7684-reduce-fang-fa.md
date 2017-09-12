{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-1WhyRedux-6-1.mp4{% endvideo %}

#Array的reduce()方法
`.reduce()`的核心思想就是它接受很多的数值作为参数，但是返回的确实一个单一的值。`.reduce()`是一个高阶函数，就是说它接受一个函数作为参数。

>##!高阶函数!
>`.map()`和`.filter()`方法同样也是高阶函数，它们接受一个函数作为它们的第一个参数。

下面看一下`.reduce()`函数的强大之处，下面有个`iceCreamStats`数组，显示了每一个队员吃了多少冰淇淋。
```
**terminal**

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