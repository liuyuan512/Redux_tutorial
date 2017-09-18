{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-2-1.mp4{% endvideo %}

##Reducer Composition
到目前为止，我们只有一个reducer。只有一个reducer可以工作，但是随着应用变得越来越大，它会很难管理。 假设我们有一个"users"的reducer:
```
function users (state = {}, action) {
  switch (action.type) {
    case 'ADD_USER' :
      return {};
    case 'REMOVE_USER':
      return {};
    default :
      return state;
  }
}
```
如果我们想要向我们的Redux store添加一个books呢？ Users和books是两种完全不同的数据。让users这个reducer来管理books的state有点不太合理。这就需要再创建一个新的reducer:
```
function users (state = {}, action) { 
  // ... 
}

function books (state = {}, action) { 
  // ... 
}
```
我们已经将我们的reducer分开来处理不同的state。这个过程叫做**reducer composition**。然而我们就会出现一个新的问题:Redux的`createScore()`方法只接收一个reducer。为了创建一个稳定的store,我们需要找出一种可以把这几个reducer组合成一个reducer的方法。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-2-2.mp4{% endvideo %}
[这里是视频中更改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/f92571e94b6b42cad3391983887261d91192a775)




