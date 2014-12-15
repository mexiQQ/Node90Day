#node90day-7

今天又學習了基礎測試庫benchmark,是一個可以測試javascript運行效率的庫（哭，接觸的東西感覺越來越高達上了）

用法：

    var suite = new Benchmark.Suite;

    // add tests
    suite.add('RegExp#test', function() {
      /o/.test('Hello World!');
    })
    .add('String#indexOf', function() {
      'Hello World!'.indexOf('o') > -1;
    })
    .add('String#match', function() {
      !!'Hello World!'.match(/o/);
    })
    // add listeners
    .on('cycle', function(event) {
      console.log(String(event.target));
    })
    .on('complete', function() {
      console.log('Fastest is ' + this.filter('fastest').pluck('name'));
    })
    // run async
    .run({ 'async': true });

ok,使用的時候照着來就行了

另外給出一個在線測試網站：http://jsperf.com/
