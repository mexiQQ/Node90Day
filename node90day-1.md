#node90day-2

##content

- eventproxy: 异步并发的管理(node最大的特性)
- superagent: 访问webservice
- cheerio: 服务端的jquery

##USE

###eventproxy

example:

				var ep = EventProxy.create("template", "data", "l10n", function (template, data, l10n) {
					_.template(template, data, l10n);
					});

				$.get("template", function (template) {
						// something
					 ep.emit("template", template);
				});
				$.get("data", function (data) {
						// something
					 ep.emit("data", data);
				});
				$.get("l10n", function (l10n) {
						// something
						ep.emit("l10n", l10n);
				});

###superagent

example:

				superagent.get("url 地址")
					.end(function(err,res){
						if(err){
							return console.error(err);
						}
						//todo somevting
				})

###cheerio

example:

				var $ = cheerio.load("html代码");
				var title  = $(title/.calss/#id).text();









