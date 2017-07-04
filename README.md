## JASMINE Test

### 简介

这是Udacity中的一个测试项目，使用了Jasmine测试框架，用以学习和展现TDD（Test Driven Development）的基本步骤和方法。

### 如何使用

下载项目后，直接打开index.html即可，jasmine组件会自动运行，并在页面的底部显示测试结果。

### 想法和思路

测试要求是渐进式的，从易到难，要测试某个对象是否为我们需要的值，需要注意先校验这个对象已经定义过(defined)。在第一次审阅者的建议下，加入了相应的正则测试url。

对于某些界面功能的测试，比如菜单是否弹出，我的思路是检验相应的CSS class是否有被添加，不过这种测试对于CSS本身有误的情况是无能为力的，我暂时没有好的解决办法，因为jasmine测试针对的是js逻辑代码，至于这个逻辑操作有没有起到相应的视觉和交互效果，似乎就无能为力了。

如果是异步测试，需要一种机制告诉测试环境异步操作已经完成，现在可以检测结果了，这个机制就是`done`函数(done这个函数名并没有特殊性，你可以起成任意名字，只是叫成done比较符合语意)。原理是这样的，在`beforeEach`函数中执行异步操作，执行完毕后就调用`done`函数发送一个信号，告诉测试环境已经OK了。这时it函数中的测试语句才会启动，来看看结果是否通过。

那怎么调用这个`done`函数呢？`beforeEach()`函数的参数是一个`function`，如果给这个`function`传入参数，则第一个参数就是我们的`done`函数，当然你可以起其它名字，比如传递参数为ddd等等。在beforeEach内的异步操作结束后，调用`done()`发送信号。为了做到这一点，可以将`done`函数作为异步操作函数的回调函数传入执行。