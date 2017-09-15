{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-4-1.mp4{% endvideo %}

##安装
如果还没有安装，先安装**react-redux**
```
npm install --save react-redux
```
一旦完成安装，你就可以从react-redux的package里引入`connect()`
```
import { connect } from 'react-redux';
```

##使用Connect

`connect()`是一个函数，它可以使得组件从Redux Store里获取state和dispatch。
```
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```
假定上面的组件`<MyComponent>`就是你想接收store state、dispatch的组件。
`mapStateToProps()`是一个接收当前store,当前props并且返回一个能被作为`<MyComponent>`的props访问的值。`mapDispatchToProps()`允许你在dispatch里面包裹action creators.下面具体看一下每一个函数

##mapStateToProps
`mapStateToProps()`可以使你指定要从store里传递给你的React组件的数据。它接收一个store的state,和一个可供选择的`ownprops`作为参数，返回的结果是一个对象。
```
mapStateToProps(state,[ownProps])
```
正如Redux官方文档里所描述的:
>“If this argument is specified, the new component will subscribe to Redux store updates. This means that any time the store is updated, mapStateToProps will be called. The results of mapStateToProps must be a plain object, which will be merged into the component’s props.”

也就是说，从`mapStateToProps()`返回的对象将会作为props传给组件。你可以把`mapStateToProps()`看做一个可以让`connect()`知道如何将store里面的部分state作为有用的props传递给组件的函数。

看下面这个例子

```
import { connect } from 'react-redux';

const User = ({ name, age }) => {
  // ...
};

const mapStateToProps = (state, props) => ({
  name: state.user.name,
  age: state.user.age
});

export default connect(mapStateToProps)(User);
```
这个例子里面，`name`和`age`都可以作为组件`User`的props被拿到。

##ownProps(可选参数)
`mapStateToProps()`的可选参数，`ownProps`可以使我们拿到connect的组件props的值。假如我们有一个子组件，它有一些从父组件传入的props:
```
<ConnectedComponent firstName={'Harper'} lastName={'Lee'} />
```
这些props可以通过`ownProps`来拿到值:
```
const mapStateToProps = (state, ownProps) => ({
  occupation: state.occupation,
  userInfo: `${ownProps.firstName} ${ownProps.lastName}: ${state.occupation}.`
});

export default connect(mapStateToProps)(MyComponent);
```
使用`ownProps`的一个经典场景就是当你需要过滤一些数据的时候。比如我们想创建一个组件，基于用户登录来渲染所有用户照片的索引。这个登录的用户的数据被存储在应用内的另外一个位置，但是被作为`MyPhotos`组件的prop传递了进来。那么我们就可以通过`ownProps`参数来获取这个值并且显示我们需要的数据:
```
const mapStateToProps = (state, ownProps) => ({
  photos: state.photos.filter(photo => photo.user === ownProps.user)
});

export default connect(mapStateToProps)(MyPhotos);

```
通过这种方式，我们可以快速将一个prop传递给组件(比如user)并且返回所有的store的state里面的`user`登录的照片。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-4-2.mp4{% endvideo %}
[此处是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/e01aeaf5719ab83cb4af8bf6aa944148335122f9)

##mapDispatchToProps()
当你connect一个组件，这个组件会被自动传入Redux的`dispatch()`方法。也就是说如果如果你想dispatch一个action，你可以在组件内部这样做:
```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { updateName } from './actions';

class User extends Component {
  state = { name: '' }
  handleUpdateUser = () => {
    this.props.boundUpdateName(this.state.name)
  }
  render () {
    // ...
  }
}

export default connect()(User);
```

`mapDispatchToProps()`可以使上面的代码整洁一点。`mapDispatchToProps()`的唯一目的就是你可以在到达组件之前将`dispatch()`绑定到你的action creators。代码:
```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { updateName } from './actions';

class User extends Component {
  state = { name: '' }
  handleUpdateUser = () => {
    this.props.boundUpdateName(this.state.name)
  }
  render () {
    // ...
  }
}

const mapDispatchToProps = dispatch => ({
  boundUpdateName: (name) => dispatch(updateName(name))
});

export default connect(null, mapDispatchToProps)(User);
```
`mapDispatchToProps()`完全是可选的，你可以选择用或者不用它。

下面看一下它是怎么工作的

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-3React&Redux-4-3.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/66a4a3ecae2d9dd4f3b20611529c4c55be19a3b2)

确保你的代码跟上了我们的节奏
![](/assets/Screen Shot 2017-09-15 at 13.04.07.png)

##练习题

![](/assets/Screen Shot 2017-09-15 at 13.05.17.png)
![](/assets/Screen Shot 2017-09-15 at 13.07.19.png)
![](/assets/Screen Shot 2017-09-15 at 13.07.39.png)

###习题3/3
下面一段代码里，组件`<ContactForm>`会接收什么值作为它的props?
```
const ContactForm = ({ firstName, handleAdd }) => (<div>...</div>);

const mapStateToProps = state => ({
  fullName: state.name
});

const mapDispatchToProps = dispatch => ({
  handleAdd: contact => dispatch(addContact(contact))
});

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(ContactForm);
```
- fullName
- mapDispatchToProps
- mapStateToProps
- contact
- handleAdd
- the entire satate

##Connect小结
`connect`把React组件和Redux的store连接起来。`mapStateToProps`允许我们指定store的哪一个state是你想传入到你的React组件的。`mapDispatchToProps`允许我们在dispatch到达组件之前将dispatch和action creators绑定在一起。

##延伸阅读
- [connect() from the react-redux docs](https://github.com/reactjs/react-redux/blob/master/docs/api.md#connectmapstatetoprops-mapdispatchtoprops-mergeprops-options)
- [connect() vs. subscribe()](https://stackoverflow.com/questions/41963225/redux-subscribe-vs-mapstatetoprops/41963751#41963751) on StackOverflow
