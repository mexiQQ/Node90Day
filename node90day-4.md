#node90day-4

今天仍然学习测试顺便捎些好东西

- superatest
- nodemon
- mocha 对于异步程序测试处理


##supertest

    var app = require('../app');
    var supertest = require('supertest');
    var request = supertest(app);

如上所示，为它的引入调用方法，专为配合express框架使用（有出入）

     It('should return 55 when n is 10', function (done) {
        // 之所以这个测试的 function 要接受一个 done 函数，是因为我们的测试内容
        // 涉及了异步调用，而 mocha 是无法感知异步调用完成的。所以我们主动接受它提供
        // 的 done 函数，在测试完毕时，自行调用一下，以示结束。
        // mocha 可以感到到我们的测试函数是否接受 done 参数。js 中，function
        // 对象是有长度的，它的长度由它的参数数量决定
        // (function (a, b, c, d) {}).length === 4
        // 所以 mocha 通过我们测试函数的长度就可以确定我们是否是异步测试。

        request.get('/fib')
        // .query 方法用来传 querystring，.send 方法用来传 body。
        // 它们都可以传 Object 对象进去。
        // 在这里，我们等于访问的是 /fib?n=10
          .query({n: 10})
          .end(function (err, res) {
            // 由于 http 返回的是 String，所以我要传入 '55'。
            res.text.should.equal('55');

            // done(err) 这种用法写起来很鸡肋，是因为偷懒不想测 err 的值
            // 如果勤快点，这里应该写成
            /*
            should.not.exist(err);
            res.text.should.equal('55');
            */
            done(err);
          });
      });

如上所示为在测试文件中使用它的方法，里边的注释很清晰明了


##nodemon

不多说，一个调试工具包，再也不用关闭node再重启了

##mocha

mocha 无法监听一步调用，需要传入一个它自己提供的done函数，用来发出结束的通知

