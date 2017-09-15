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



