# Node.JS

node.js只是一个运行环境

文件下载地址：https://nodejs.org/en/download/

![image-20210503155945051](D:\LJ\git\git_project\Study_Notes\img\2-node_js.png)

使用node -v 可查看软件是否安装成功，以及安装的版本

## 1.NVM安装和使用：

  搭建方式:
	1.下载NVM: https://github.com/coreybutler/nvm-windows
	2.在D盘创建dev目录
	3.在Dev目中中创建两个子目录nvm和nodejs, 并且把nvm包解压进去nvm目录中
	4.在install.cmd文件上面右键选择【以管理员身份运行】
 	 在终端中直接按下回车
  	将弹出的文件另存为到NVM目录
  	打开settings.txt文件. 修改
 	 root: D:\Developer\Dev\NVM
	  path: D:\Developer\Dev\Node
	5.配置环境变量
       NVM_HOME: D:\Developer\Dev\NVM
      NVM_SYMLINK: D:\Developer\Dev\Node
     在Path中添加 %NVM_HOME% %NVM_SYMLINK%
   6.在命令行工具中输入 nvm version

   NVM常用命令
- nvm list 查看当前安装的Node.js所有版本
- nvm install 版本号 安装指定版本的Node.js
- nvm uninstall 版本号 卸载指定版本的Node.js
- nvm use 版本号 选择指定版本的Node.js

## 2.NodeJS代码执行

​    1.可以直接在命令行工具中编写执行JS代码（REPL----Read Eval  Print  Loop:交互式解释器）

   2.找到需要执行的JS文件，在地址栏输入cmd 进入命令提示符，使用node  JS文件即可执行

## 3.CommonJS规范

 CommonJS规范规定了如何定义一个模板，如何暴露模板中的变量函数，以及如何使用定义好的模板

  -在CommonJS规范中每一个文件就是一个模板

 -在CommonJS规范中每个文件中的变量函数都是私有的，对其他文件不可见

-在CommonJS规范中每个文件中的变量函数必须通过exports暴露之后其他文件才可以使用

-在在CommonJS规范中想要使用其他文件暴露的变量函数必须通过require（）导入模块才可以使用。

## 4.模块导出数据的几种方式

1.exports.xxx=xxx

2.module.exports.xxx=xxx

3.global.xxx=xxx

不过使用哪种方式，都必须用require导入才能使用，通过第三种方式不符合CommonJS规范，不推荐使用。

```
exports和modules.exports的区别：后者可直接赋值
```



## 5.NPM包安装方式

    - 全局安装  (一般用于安装全局使用的工具, 存储在全局node_modules中)
        npm install -g 包名   (默认安装最新版本)
        npm uninstall -g 包名
        npm update -g 包名   (更新失败可以直接使用install)
    
    - 本地安装 (一般用于安装当前项目使用的包, 存储在当前项目node_modules中)
    npm install 包名
    npm uninstall 包名
    npm update 包名
    
    2.初始化本地包
    npm init   ->  初始化package.json文件
    npm init -y -> 初始化package.json文件
    
    npm install 包名 --save
    npm install 包名 --save-dev
    
    包描述文件 package.json, 定义了当前项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。
    npm install 命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境
    注意点:package.json文件中, 不能加入任何注释
    
    - dependencies：生产环境包的依赖，一个关联数组，由包的名称和版本号组成
    - devDependencies：开发环境包的依赖，一个关联数组，由包的名称和版本号组成
    
    1.将项目拷贝给其它人, 或者发布的时候, 我们不会将node_modules也给别人, 因为太大
    2.因为有的包可能只在开发阶段需要, 但是在上线阶段不需要, 所以需要分开指定
    
    npm i               所有的包都会被安装
    npm i --production  只会安装dependencies中的包
    npm i --development  只会安装devDependencies中的包

## 6.Buffee中创建实例的方法和常用的属性

   1.什么是Buffer?
    Buffer是NodeJS全局对象上的一个类, 是一个专门用于存储字节数据的类
    NodeJS提供了操作计算机底层API, 而计算机底层只能识别0和1,
    所以就提供了一个专门用于存储字节数据的类

   2.如何创建一个Buffer对象
     2.1创建一个指定大小的Buffer
     Buffer.alloc(size[, fill[, encoding]])//size表示大小，fill表示填充，encoding表示编码方式

​     2.2根据数组/字符串创建一个Buffer对象
​          Buffer.from(string[, encoding])

​      3.Buffer对象本质
​       本质就是一个数组

```
let buf = Buffer.alloc(5);
console.log(buf); // <Buffer 00 00 00 00 00>
// 注意点: 通过console.log();输出Buffer. 会自动将存储的内容转换成16进制再输出

let buf = Buffer.alloc(5, 17);
console.log(buf); <Buffer 11 11 11 11 11>使用11来填充数据

let buf = Buffer.from("abc");
console.log(buf); // <Buffer 61 62 63>

let buf = Buffer.from([1, 3, 5]);
console.log(buf);
console.dir(buf);// Buffer(3) [Uint8Array] [ 1, 3, 5 ]
buf[0] = 6;
console.log(buf);
```

实例方法：

  1.将二进制数据转换成字符串
     返回: <string> 转换后的字符串数据。
	buf.toString();

2.往Buffer中写入数据

![image-20210506113619728](D:\LJ\git\git_project\Study_Notes\img\3-Buffer写入数据.png)

​	string <string> 要写入 buf 的字符串。
​	offset <integer> 开始写入 string 之前要跳过的字节数。默认值: 0。
​	length <integer> 要写入的字节数。默认值: buf.length - offset。
​	encoding <string> string 的字符编码。默认值: 'utf8'。
​	返回: <integer> 已写入的字节数。
​	buf.write(string[, offset[, length]][, encoding])

3.从指定位置截取新Buffer
	start <integer> 新 Buffer 开始的位置。默认值: 0。
	end <integer> 新 Buffer 结束的位置（不包含）
	buf.slice([start[, end]])

```
let buf = Buffer.from([97, 98, 99]);
console.log(buf);
console.log(buf.toString());

let buf = Buffer.alloc(5); // <Buffer 00 00 00 00 00>
console.log(buf);
buf.write("abcdefg");
buf.write("abcdefg", 2);//从索引为2开始输出，前面默认为0
buf.write("abcdefg", 2, 2);
console.log(buf);
console.log(buf.toString());

let buf1 = Buffer.from("abcdefg");
let buf2 = buf1.slice();
let buf2 = buf1.slice(2);
let buf2 = buf1.slice(2,4);
console.log(buf2);
console.log(buf2.toString());
```

静态方法：

1.检查是否支持某种编码格式
	Buffer.isEncoding(encoding)

2.检查是否是Buffer类型对象
	Buffer.isBuffer(obj)

3.获取Buffer实际字节长度
	Buffer.byteLength(string[, encoding])
	注意点: 一个汉字占用三个字节

4.合并Buffer中的数据
	Buffer.concat(list[, totalLength])

```
let res = Buffer.isEncoding("gbk");
 console.log(res); //false,默认是utf-8

let obj = Buffer.alloc(5);
let res = Buffer.isBuffer(obj);
console.log(res);//Ture

let buf = Buffer.from("知播渔");
let res = Buffer.byteLength(buf);
console.log(res);//9
console.log(buf.length);//9

let buf1 = Buffer.from("123");
let buf2 = Buffer.from("abc");
let buf3 = Buffer.from("xxx");
let res = Buffer.concat([buf1, buf2, buf3]);
console.log(res);//<Buffer 31 32 33 61 62 63 78 78 78>
console.log(res.toString());//123abcxxx
```

NodeJS核心API-Path方法，详见网址——Node.js v14.16.1 文档：http://nodejs.cn/api

* ```
  //导入“path”系统模块
  let path = require("path");
  
  // basename用于获取路径的最后一个组成部分
  let res = path.basename('/a/b/c/d/index.html');//index.html
  let res = path.basename('/a/b/c/d');//d
  let res = path.basename('/a/b/c/d/index.html', ".html");//index
  
  // dirname用于获取路径中的目录, 也就是除了最后一个部分以外的内容
  let res = path.dirname('/a/b/c/d/index.html');//a/b/c/d
  
  extname用于获取路径中最后一个组成部分的扩展名
  let res = path.extname('/a/b/c/d/index.html');//.html
  let res = path.extname('/a/b/c/d');//空
  
  /*
  isAbsolute用于判断路径是否是一个绝对路径
  注意点:
  区分操作系统
  在Linux操作系统中/开头就是绝对路径
  在Windows操作系统中盘符开头就是绝对路径
  
  在Linux操作系统中路径的分隔符是左斜杠 /
  在Windows操作系统中路径的分隔符是右斜杠 \
  */
  
  let res = path.isAbsolute('/a/b/c/d/index.html'); // true
  let res = path.isAbsolute('./a/b/c/d/index.html'); // false
  let res = path.isAbsolute('c:\\a\\b\\c\\d\\index.html'); // true
  
  // path.sep用于获取当前操作系统中路径的分隔符的
  如果是在Linux操作系统中运行那么获取到的是 左斜杠 /
  如果是在Windows操作系统中运行那么获取到的是 右斜杠 \
  console.log(path.sep);
  
  // path.delimiter用于获取当前操作系统环境变量的分隔符的
  如果是在Linux操作系统中运行那么获取到的是 :
  如果是在Windows操作系统中运行那么获取到的是 ;
  console.log(path.delimiter);
  
  /*
  path.parse(path): 用于将路径转换成对象
  {
    root: '/',
    dir: '/a/b/c/d',
    base: 'index.html',
    ext: '.html',
    name: 'index'
  }
  path.format(pathObject): 用于将对象转换成路径
   */
   
    /*
  let obj = path.parse("/a/b/c/d/index.html");
  
  let obj = {
      root: '/',
      dir: '/a/b/c/d',
      base: 'index.html',
      ext: '.html',
      name: 'index'
  };
  let str = path.format(obj);// /a/b/c/d\index.html
   */
  
  /*
  path.join([...paths]): 用于拼接路径
  注意点:
  如果参数中没有添加/, 那么该方法会自动添加
  如果参数中有.., 那么会自动根据前面的参数生成的路径, 去到上一级路径
   */
   
    /*
   let str = path.join("/a/b", "c"); // /a/b/c
   let str = path.join("/a/b", "/c"); // /a/b/c
   let str = path.join("/a/b", "/c", "../"); // /a/b/c --> /a/b
    // let str = path.join("/a/b", "/c", "../../"); // /a/b/c --> /a
     */
  
  
  //path.normalize(path): 用于规范化路径
    /*
    let res = path.normalize("/a//b///c////d/////index.html");
    console.log(res); // /a/b/c/d/index.html
    */
  
  /*
  path.relative(from, to): 用于计算相对路径
  第一个参数: /data/orandea/test/aaa
  第二个参数: /data/orandea/impl/bbb
  
  /data/orandea/test/aaa --> ../  --> /data/orandea/test
  /data/orandea/test --> ../ --> /data/orandea
  */
  
  
  let res = path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');//..\..\impl\bbb
  
  //.resolve([...paths]): 用于解析路径
  注意点: 如果后面的参数是绝对路径, 那么前面的参数就会被忽略
  let res = path.resolve('/foo/bar', './baz'); // /foo/bar/baz
   let res = path.resolve('/foo/bar', '../baz'); // /foo/baz
   let res = path.resolve('/foo/bar', '/baz'); // /baz
    console.log(res);
  ```

  NodeJS核心API-fs
  
  ```
  let fs = require("fs")
  let path = require("path")
  
  /*
  1、文件状态
  console.log(1);
  fs.stat(__dirname,function (err,stats) {
      // console.log(3);
      // console.log(err);
      if (stats.isFile()){
          console.log("这是一个文件");
      }else if (stats.isDirectory()){
          console.log("这是一个文件夹");
      }
  })
  console.log(fs.statSync(__filename));
  console.log(2);*/
  
  /*
  2.文件读取
  let str = path.join(__dirname,"lj.txt")
  console.log(str);
  fs.readFile(str,function(err,data){
      if(err) {
          throw new Error("读取文件失败")
      }
      console.log(data.toString());
  })
  console.log(fs.readFileSync(str,"utf8"));*/
  
  /*
  3.文件写入
  let str = path.join(__dirname,"ll.txt")
  let buf = Buffer.from("我有一只小毛驴，从来也不骑")
  fs.writeFile(str,buf,"utf-8",function (err){
      if(err){
          throw new Error("写入数据失败")
      }
      console.log("成功写入数据");
  })*/
  
  /*
  4.向文件中追加数据
  let str = path.join(__dirname,"ll.txt")
  let buf = Buffer.from("我有一只小毛驴，从来也不骑")
  fs.appendFile(str,buf,"utf-8",function (err){
      if(err){
          throw new Error("追加数据失败")
      }
      console.log("成功追加数据");
  })*/
  /*
  5.表示分批读取数据
  //拼接读取的路径
  let str = path.join(__dirname,"ll.txt")
  //创建一个读取流
  let readStream = fs.createReadStream(str,{encoding:"utf8",highWaterMark:1});
  //3.添加事件监听
  readStream.on("open",function () {
      console.log("表示数据流和文件建立关系成功");
  })
  readStream.on("error",function () {
      console.log("表示数据流和文件建立关系失败");
  })
  readStream.on("data",function (data) {
      console.log("表示通过读取流从文件中读取到数据"+data);
  })
  readStream.on("close",function () {
      console.log("表示数据流断开了和文件的关系，并且数据也读取成功了");
  
  })*/
  
  /*
  6.表示分批写入数据
  let str = path.join(__dirname,"lj.txt")
  let writeStream = fs.createWriteStream(str,{encoding:"utf8"});
  
  writeStream.on("open",function () {
      console.log("表示数据流和文件建立关系成功");
  })
  writeStream.on("error",function () {
      console.log("表示数据流和文件建立关系失败");
  })
  writeStream.on("close",function () {
      console.log("表示数据流断开了和文件的关系，并且数据也读取成功了");
  })
  let data = "movie.douban.com"
  let index = 0
  let timeId = setInterval(function () {
      let ch = data[index]
      index++
      writeStream.write(ch)
      console.log("本次写入了" + ch);
      if(index == data.length){
          clearInterval(timeId)
          writeStream.end()
      }
  },500)*/
  
  
  /*
   7.实现文件的拷贝
  
  //  读取文件路径
  let readpath = path.join(__dirname,"ll.txt")
  //  写入文件路径
  let writepath = path.join(__dirname,"jj.txt")
  //  创建读入流
  let readStream = fs.createReadStream(readpath,{encoding:"utf8"})
  //  创建写入流
  let writeStream = fs.createWriteStream(writepath,{encoding:"utf8"})
  //  添加事件监听
  readStream.on("open",function (){
      console.log("表示数据流和文件建立关系成功");
  })
  readStream.on("error",function (){
      console.log("表示数据流和文件建立关系失败");
  })
  readStream.on("data",function (data){
      writeStream.write(data)
  })
  readStream.on("close",function (){
      console.log("表示数据流断开了和文件的关系，并且数据也读取成功了");
      writeStream.end()
  })
  writeStream.on("open",function (){
      console.log("1\表示数据流和文件建立关系成功");
  })
  writeStream.on("error",function (){
      console.log("2\表示数据流和文件建立关系失败");
  })
  writeStream.on("close",function (){
      console.log("3\表示数据流断开了和文件的关系，并且数据也读取成功了");
  })
   */
  ```