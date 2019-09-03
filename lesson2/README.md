## 学习使用外部模块

#### 目标
当在浏览器中访问 http://localhost:3000/?q=alsotang 时，输出 alsotang 的 md5 值，即 bdd5e57b5c0040f9dc23d430846e68a3。

#### 挑战
访问 http://localhost:3000/?q=alsotang 时，输出 alsotang 的 sha1 值，即 e3c766d71667567e18f77869c65cd62f6a1b9ab9。

#### 知识点
1. 学习req.query的用法
2. 学习建立package.json来管理Node.js项目

#### 课程内容
习惯了每个项目里面基本都是有个package.json文件的。所以，接下来我要告诉你们package.json这个文件的用法了。

简单来说，这个package.json文件就是定义了项目的各种元信息。包括项目的名称，git repo的地址，作者等等。最重要的是，其中定义了项目的依赖。这样，项目在部署时，就不必将node_modules目录也上传到服务器。服务器在拿到我i们的项目时，只需要npm install，就能把所有的依赖都安装在node_modules下面了。

我们在新建一个项目的时候，为了生成package.json文件，我们可以执行：npm init。
npm init 这个命令的作用就是帮我们互动式地生成一份最简单的 package.json 文件，init 是 initialize 的意思，初始化。

当乱填信息完毕之后，我们的目录下就会有个 package.json 文件了。我们就可以安装我们项目中所需要用到的依赖了。
安装依赖的时候-save 参数，这个参数的作用就是在你安装依赖的同时，自动把这些依赖写入package.json。命令执行完成之后，查看 package.json，会发现多了一个 dependencies 字段。查看 node_modules 目录，会发现有dependencies里面的依赖文件。


我们开始写应用层的代码，建立一个 app.js 文件，复制以下代码进去：
```
// 引入依赖
var express = require('express');
var utility = require('utility');

// 建立 express 实例
var app = express();

app.get('/', function (req, res) {
  // 从 req.query 中取出我们的 q 参数。
  // 如果是 post 传来的 body 数据，则是在 req.body 里面，不过 express 默认不处理 body 中的信息，需要引入 https://github.com/expressjs/body-parser 这个中间件才会处理，这个后面会讲到。
  // 如果分不清什么是 query，什么是 body 的话，那就需要补一下 http 的知识了
  var q = req.query.q;

  // 调用 utility.md5 方法，得到 md5 之后的值
  // 之所以使用 utility 这个库来生成 md5 值，其实只是习惯问题。每个人都有自己习惯的技术堆栈，
  // 我刚入职阿里的时候跟着苏千和朴灵混，所以也混到了不少他们的技术堆栈，仅此而已。
  // utility 的 github 地址：https://github.com/node-modules/utility
  // 里面定义了很多常用且比较杂的辅助方法，可以去看看
  var md5Value = utility.md5(q);

  res.send(md5Value);
});

app.listen(3000, function (req, res) {
  console.log('app is running at port 3000');
});

```

OK，运行我们的程序

$ node app.js

访问 http://localhost:3000/?q=alsotang，完成。


#### 温馨提示
如果直接访问 http://localhost:3000/ 会抛错。

这是因为，当我们不传入 q 参数时，req.query.q 取到的值是 undefined，utility.md5 直接使用了这个空值，导致下层的 crypto 抛错。
