#React&Redux

到目前为止，我们学习了通过给`createStore()`传递一个reducer函数来创建store。然后我们学习了如何使用`dispatch()`, `getState()`, 和 `subscribe()`来连接起来React和Redux。或许你注意到了：这种工作方式并不是那么理想。我们把store传入了主组件，这样组件就可以拿到`dispatch()`, `getState()`, 和 `subscribe()`了。这种方法对于小的应用还好，一旦应用变得复杂，有了额外的组件，这种方式就没有那么方便了。

但是这并不意味着Redux是没有效率的，我们只是没有使用好的方法。直到这里，我们一直学习的是Redux的底层方法，并且尽量用在React上。那么有没有一种更好一点的抽象方法，专门用在Redux和React的连接上呢？ 好消息，是有的。叫做:`react-redux`，这是redux的创建者发明的。

`react-redux`最大的益处体现在当你dispatching你的actions，以及从React组件内部访问Redux store的时候。这些因为`react-redux`的`Provider`组件和`connect()`方法成为可能。

`connect()`让你可以实现哪个组件应该接收来自store的哪个state，而`Provider`可以保障`connect()`工作的很顺利。下面就深入的看一下。