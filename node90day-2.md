首先我先来分享一个模拟web服务，从alsotang同学的Demo中学习到的

如下所示:

    // 并发连接数的计数器
    var concurrencyCount = 0;
    var fetchUrl = function (url, callback) {
      // delay 的值在 2000 以内，是个随机的整数
      var delay = parseInt((Math.random() * 10000000) % 2000, 10);
      concurrencyCount++;
      console.log('现在的并发数是', concurrencyCount, '，正在抓取的是', url, '，耗时' + delay + '毫秒');
      setTimeout(function () {
        concurrencyCount--;
        callback(null, url + ' html content');
      }, delay);
    };

# async包的使用

mapLimit(arr, limit, iterator, callback)

- arr: An array to iterate over.
- limit: The maximum number of iterators to run at any time.
- iterator: A function to apply to each item in arr. The iterator is passed a callback(err, transformed) which must be called once it has completed with an error (which can be null) and a transformed item.
- callback: A callback which is called when all iterator calls have finished, or an error occurs. The result is an array of the transformed items from the original arr.

example:

    <sync.mapLimit(urls, 5, function (url, callback) {
      fetchUrl(url, callback);
    }, function (err, result) {
      console.log('final:');
      console.log(result);
    });







