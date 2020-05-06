# 【翻译】JavaScript之回调

[原文链接](https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced)

#### 什么是回调函数

简单来说，回调函数就是：只有等另一个函数执行完了才可以执行的函数。

复杂点说，在JavaScript中，函数都是对象， 因此在函数中可以将函数作为参数传递，也可以作为返回值；这样的函数也称为高阶函数，任何一个将函数作为参数传递的函数都称为回调函数。

话不多说，直接看例子吧。

#### 为什么需要回调

最重要的一个原因就是JavaScript是事件驱动语言，这意味着JavaScript在监听其他事件时会持续执行而不是在执行前一直等待响应，看下面这个例子：

```javascript
function first() {
  console.log(1);
}

function second() {
  console.log(2)
}

first();
second();
```

如你所料，first函数首先被执行，second函数其次被执行 ——打印结果如下：

```text
// 1
// 2
```

现在看来没什么毛病 但是，当first函数包含了一些不能立马被执行的代码时会怎样呢？比如，当我们发送了一个需要等待响应的API请求时。我们将用setTimeout\(一个在设置了指定时间之后调用函数的js内置方法\)来模拟这个操作，我们把函数延迟500ms执行来模拟API请求，新代码如下：

```javascript
function first() {
  setTimeout(function(){
     console.log(1);
  }, 500)
}

function second() {
  console.log(2)
}

first();
second();
```

现在明不明白setTimeout的工作原理不重要，重要的是你看到我们把console.log\(1\)放到了500ms的延迟内，那现在调用函数会发生什么呢？

```javascript
first();
second();
// 2
// 1
```

虽然我们先调用了first\(\)函数，但是其结果却在second\(\)函数之后打印出来。 并不是JavaScript没有按照我们想要的顺序执行，而且Javascript没有等到first函数响应就已经往下执行second\(\)函数了。

为什么看到的是这个结果呢？因为你不可能一个一个调用函数且希望它们按序执行，回调函数是一个能让某些代码在其他代码执行完成前不会被执行的方法。

#### 创建一个回调函数

话不多说，秀代码！ 首先，打开chrome浏览器的console界面\(Windows：`ctrl` + `shift` + `j`，Mac：cmd + option + j\)并输入下面的函数声明:

```text
function doHomework(subject) {
  alert(`Starting my ${subject} homework`)
}
```

上面我们创建了一个`doHomework`函数，这个函数需要传入一个科目参数，在控制台输入以下代码调用该函数：

```text
doHomework('math'); // Alerts：Starting my math homework.
```

现在来添加一个回调——作为`doHomework`的最后一个参数我们用callback关键字来传递，然后在调用doHomework的第二个参数中定义回调函数的第二个参数。

```javascript
function doHomework(subject, callback) {
  alert(`Starting my ${subject} homework`);
  callback();
}
doHomework('math', function() {
  alert('Finished my homework');
});
```

如果你在控制台输入了上面那些代码你会依次看到两个警示框弹出，starting homework 在finished homework之前。

其实回调函数没必要每次都在调用函数时声明，可以 在其他地方声明，比如：

```javascript
function doHomework(subject, callback) {
  alert(`Starting my ${subject} homework.`);
  callback();
}
function alertFinished(){
  alert('Finished my homework');
}
doHomework('math', alertFinished);
```

这个例子的结果和上面那个例子是一样的，只是设置的不一样，在调用doHomework时我们把alertFinished函数名作为参数传递了。

#### 真实案例

上周我发布了一篇名为[Build a simple Twitter Bot in 38 lines of code](https://hackernoon.com/build-a-simple-twitter-bot-with-node-js-in-just-38-lines-of-code-ed92db9eb078)的文章，那篇文章 中的代码生效的原因就在于[Twitters API](https://developer.twitter.com/en/docs)，当你请求API时，在你操作响应结果之前你必须等待响应。这在真实场景中是一个很好的回调例子，下面是请求的代码：

```javascript
T.get('search/tweets', params, function(err, data, response) {
  if(!err){
    // 这是见证奇迹的地方
  } else {
    console.log(err);
  }
})
```

* T.get意味着我们将要向Twitter发起一个get请求
* 这个请求有三个参数：‘search/tweets’是我们要请求的路径，params是查询参数，最后那个匿名函数就是我们的回调

回调在这里很重要因为我们需要等待服务器的响应才能继续我们的代码，我们也不知道API请求成功与否，所以在通过get请求向search/tweets 发送参数后只能等待，一旦Twitter 响应了回调函数就会被调用，然后发送一个err对象或者response对象给我们。在回调函数内我们可以用 if 语句判断请求是否成功，从而操作新数据。

#### 你可以的

很棒，你现在可以理解回调函数是什么以及它是如何运行的了。这仅仅只是回调函数的冰山一角，还有很多需要学习的。

