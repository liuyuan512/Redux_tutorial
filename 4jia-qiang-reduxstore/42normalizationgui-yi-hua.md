{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-4ArchitectReduxStore-3-1.mp4{% endvideo %}

##创建一个高效的Redux Store
当构建一个Redux store时，有两个原则应当牢记:
    1. **不要重复数据**。如果数据存在于很多地方，那么你就没有了唯一数据源，并且还得浪费精力来保持数据同步
    2. **使你的store结构皆可能的简单**。嵌套的数据会使reducer的逻辑更加复杂。
    
下面看一个简单的例子。下面是我们有一个`people`对象和一个`friends`数组:
```js
const people = {
  kassidi: {
    name: 'Kassidi Henry',
    age: 24,
    favoriteMovie: 'Remember the Titans'
  },
  tyler: {
    name: 'Tyler McGinnis',
    age: 25,
    favoriteMovie: 'Fatigue: A JavaScript Story'
  },
  jake: {
    name: 'Jake Lingwall',
    age: 26,
    favoriteMovie: 'Casablanca'
  },
}

const friends = ['kassidi', 'jake']
```
现在假设我们需要创建一个数组，这个数组里的每个元素都是对应的`people`的每一个对象，代码很简单：
```
friends.map((friend) => people[friend])
```
这样一来，就不会产生数据一致性错误，因为我所有的数据都只是指向了另一个数据。这就是Redux里的data的正确工作方式。要尽可能的避免数据重复，要用数据指引来替代。

这个模式在Redux文档里是这样描述的:
>"In a more complex app, you’re going to want different entities to reference each other. We suggest that you keep your state as normalized as possible, without any nesting. Keep every entity in an object stored with an ID as a key, and use IDs to reference it from other entities, or lists."

下一个原则就是尽量使你store里的state简单，就是不要嵌套那么多层。因为这样做可以减少复杂度，提高性能。

假设我们有一个这样的对象:
```js
const books = {
  fiction: {
    fantasy: {
      0: {
        title: 'Harry Potter and the Nested Data',
        author: 'JK Rowling'
      }
    },
    romance: {},
    scifi: {}
  },
  nonFiction: {}
};
```

假设我们想要创建一个新的对象(因为我们不能直接修改原来的state)，但是修改了Harry Potter的title，那我们的reducer将会像这样:
```js
function books (state, action) {
  const { bookType, genre, id, title } = action
  if (action.type = CHANGE_TITLE) {
    return {
      ...state,
      [bookType]: {
        ...state[bookType],
        [genre]: {
          ...state[bookType][genre]: {
            [id]: {
              ...state[bookType][genre][id],
              title,
            }
          }
        }
      }
    }
  }

  return state
}
```

看一下这嵌套的结构！这样不仅没有效率，而且很难理解，对写代码的和看代码都是。

通过指引不同的实体到你state里，并且保持state尽可能的简洁，到达了提升性能和使你代码更容易理解的目的。

##Normalization(归一化)小结
**Normalization**就是指移除重复的数据，和让你的数据尽可能的没有那么多的嵌套。这样以来，应用不但保持了唯一数据源的原则，而且也使得更新state变得整洁和容易。最终，归一化你的Redux store会变得更加高效。

##延伸阅读
- [Normalizr](https://github.com/paularmstrong/normalizr)
- [Normalizing State Shape](http://redux.js.org/docs/recipes/reducers/NormalizingStateShape.html)from the Redux docs

