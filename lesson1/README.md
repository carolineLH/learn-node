## 一个最简单的express应用
#### 目标
建立一个lesson1项目，在其中编写代码。当在浏览器中访问http://localhost:3000/ 时，输出 Hello World。

#### 挑战
访问http://localhost:3000/ 时，输出 你好，世界。

#### 知识点
1. 包管理器npm。使用npm安装包，并自动安装所需依赖。
2. 框架express。学习新建express实例，并定义routes，产生输出。

#### 包管理器npm
npm可以自动管理包依赖，只需要你安装你想要的包，不必考虑这个包的依赖包。
在Node.js中，对应就是npm，npm是Node.js Package Manager的意思。

#### 框架Express
express是Node.js应用最广泛的web框架，它非常薄。

* 我们需要得到一个express，进入到lesson1文件夹，在里面安装express：
```
cd lesson1

npm install express --registry=https://registry.npm.taobao.org
```
安装完成之后，lesson1目录下会出现一个node_modules文件夹，node_modules文件夹里面也会出现一个express文件夹。说明安装成功。

* 新建一个app.js文件
在app.js文件中写入这些代码：
```
// 这句的意思就是引入 `express` 模块，并将它赋予 `express` 这个变量等待使用。
var express = require('express');
// 调用 express 实例，它是一个函数，不带参数调用时，会返回一个 express 实例，将这个变量赋予 app 变量。
var app = express();

// app 本身有很多方法，其中包括最常用的 get、post、put/patch、delete，在这里我们调用其中的 get 方法，为我们的 `/` 路径指定一个 handler 函数。
// 这个 handler 函数会接收 req 和 res 两个对象，他们分别是请求的 request 和 response。
// request 中包含了浏览器传来的各种信息，比如 query 啊，body 啊，headers 啊之类的，都可以通过 req 对象访问到。
// res 对象，我们一般不从里面取信息，而是通过它来定制我们向浏览器输出的信息，比如 header 信息，比如想要向浏览器输出的内容。这里我们调用了它的 #send 方法，向浏览器输出一个字符串。
app.get('/', function (req, res) {
  res.send('Hello World');
});

// 定义好我们 app 的行为之后，让它监听本地的 3000 端口。这里的第二个函数是个回调函数，会在 listen 动作成功后执行，我们这里执行了一个命令行输出操作，告诉我们监听动作已完成。
app.listen(3000, function () {
  console.log('app is listening at port 3000');
});
```
* 执行 node app.js

这时候我们的 app 就跑起来了，终端中会输出 app is listening at port 3000。这时我们打开浏览器，访问 http://localhost:3000/，会出现 Hello World。如果没有出现的话，肯定是上述哪一步弄错了，自己调试一下。
* 想要完成我们的挑战的话，只需要将res.send('Hello World');改成res.send('你好，世界');

#### 补充知识
在这个例子中，node代码监听了3000端口，用户通过访问http://localhost:3000/ 得到了内容，为什么呢？

###### 端口
端口的作用：通过端口来区分出同一电脑内不同应用或者进程，从而实现一条物理网线(通过分组交换技术-比如internet)同时链接多个程序。

