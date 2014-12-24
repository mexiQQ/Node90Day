#node90day-10

经过9天的node-lesson学习，相信你也看出这是一门偏于实践的课程，对于有经验的开发者，几乎没有多少帮助，除了介绍的几个库，直接把库总结一下就好了嘛 2333333(纯属扯淡)

# node90day之异步编程的美和疾

- 单线程
- 异步IO

node 是单线程的非同步I/O的

解释：

- 多线程带来了上下文切换的开销，以及实际编程时的锁和线程之间的同步问题
- 同步IO符合人类的思维习惯（个人觉的不符实，要看人的）,但是性能上远远比不上异步IO，自己想想很容易明白，比如你愿意等一个吃饭总是慢别人半小时的同学吗

### node异步编程的优势
(Node最大的特性：基于事件驱动的非阻塞IO)

- 高并发，云服务的兴起由此带来的问题就是高并发的接口访问量，想想就应该明白它的意义
- 善于I/O密集型应用的它在不影响异步I/O 调用的情况下可以用在任何地方（由于计算密集型应用占用CPU时间片的时间太长，导致无法进行异步IO调用的安排）
- node的单线程相当于管家，IO线程池相当于小二（node的底层还是调用系统级的IO多线程）

### node异步编程的劣势

1. 异常处理

try/catch/default模式只能检测事件循环的异常，而异步编程和基于事件的模式导致了很多事件（回调函数）在后一个或者后面某个事件循环中执行，所以不活不到

那么问题来了，如何对这种异常进行检测呢？

node提供了一些自己编写异步方法的原则：

- 必须执行掉入者传入的回调函数
- 如果发生异常要传递回异常供调用者判断

给出一个的例子：

var interview = function(callback){
  process.nextTick(function(){
    var resutlt = something;
    if(error){
      callback(error);
    }else{
      callback(null,result);
    }
  })
}

给出一个读取本地配置文件的示例：
var fs = require('fs');
var readLocalSetting = function(callback){
  //node读取本地文件本来就有个异步方法
  fs.redFile('/etc/setting', function (err, data) {
  if (err) callback(err);
    callback(null,data);
  });
}












