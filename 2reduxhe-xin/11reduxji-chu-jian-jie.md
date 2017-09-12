{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-2-1.mp4{% endvideo %}
浏览器允许你设立事件监听器和对某些事件进行响应。Redux同样，只是这些事件被称为**actions**。这些你创建的actions是信息的载体，用来描述应用里应该更新state的任何的事件。

{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-2-2.mp4{% endvideo %}
Actions只是一个JavaScript对象，用来描述应当更新的state的任何事件。这些对象里应当包含一个`type`属性，为了区别每一种事件类型。
```
const LOAD_PROFILE = 'LOAD_PROFILE';

const myAction = {
  type: LOAD_PROFILE
};
```
表示所发生的操作类型所需要的任何其它数据都可以作为action中的属性传递。

>##!Action 建议!
>一些你在创建Action 对象时需要注意的
>- action的`type`属性尽量用常量表示，而不要用字符串。当然常亮和字符串都可以工作，但是当使用常量的时候，如果发生拼写错误就会在console里抛出一个错误，但是字符串就会没有任何反应。
- 尽可能使你的信息载体小一点。使你的资源仅传递必要的data。

![](/assets/Screen Shot 2017-09-12 at 17.34.49.png)

##Action Creators
尽管Redux actions只是JavaScript对象，但是这些对象并不很方便。为了使这些actions更加方便和易于测试，我们可以把它包装在函数里。这些函数被称为**actions creators**.actions creators只是创建并返回一个action。
```
const submitUser = user => ({
  type: SUBMIT_USER,
  user
});
```

现在，每当我们需要一个`SUBMIT_USER`action，我们就可以调用`submitUser()`函数，给它传递一个user参数，它就会产生一个action！

##练2/2
创建一个叫做"mealCreator"的Action Creator，应当包含：
- 接受一个id
- 返回一个Redux action,有一个type属性，值为:CREATE_MEAL
- 包含一个作为参数传递进来的id

##开始项目
下面我们开始创建一个称为Udacimeals的项目。这个应用会拥有可定制的日历来让用户可以记录一周内的每一天的早餐、午餐和晚餐。用户将利用[ Edamam's Recipe Search API](https://developer.edamam.com/edamam-recipe-api)来添加餐点，然后生成一个基于选择的餐点的购物清单。

我们将首先编写代表在应用程序中更改状态的两种action开始:
1. 增加一个新的食谱
2. 从日历中删除食品

我们将使用[Create React App](https://github.com/facebookincubator/create-react-app)来构建应用程序。确保你安装了它，然后创建一个新的app.

[这里是项目框架的commit](https://github.com/udacity/reactnd-udacimeals-complete/commit/6c458c57016e56c8e5f29c20a84dd705ea632cc8)

开始下一步之前，我们先确保以下几步你都做了

- 安装了[Create React App](https://github.com/facebookincubator/create-react-app)
- 利用`Create React App`创建了`Udacimeals`项目
- 在`src`文件夹里创建了`actions`,`components`和`utils`文件夹
- 移除了`components`文件夹里的`App.js`
- 在`utils`文件夹里面创建了`api.js`和`helper.js`文件([文件内容看这里](https://github.com/udacity/reactnd-udacimeals-complete/tree/6c458c57016e56c8e5f29c20a84dd705ea632cc8/src/utils))


{% video %}http://ovwbdgz95.bkt.clouddn.com/react-redux-2ReduxAtItsCore-2-3.mp4{% endvideo %}
[这里是视频里修改的代码](https://github.com/udacity/reactnd-udacimeals-complete/commit/53bebcf6ce77202e1dd83ec255a70f5da8e73239)

![](/assets/Screen Shot 2017-09-12 at 18.23.49.png)

##小结
在这一小节，我们


