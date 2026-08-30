
> Name

Function automatic fault tolerance template
> Author

Zero

> Strategy Description

After ticking this template and calling this template, the specified Api function will automatically be retried and fault-tolerant, and multiple exchanges can be supported.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|RetryInterval|500|Fault tolerance retry interval (milliseconds)|
|Debug|true|Show retry records|
|EnableErrorFilter|false|Shield common network error messages|
|ApiList|GetAccount,GetDepth,GetTicker,GetRecords,GetTrades,GetOrders,SetContractType|Fault-tolerant API list|

> Source (javascript)

``` javascript
// 模板初始化时调用
function init() {
    // 过滤常见错误
    if (EnableErrorFilter) {
        SetErrorFilter("502:|503:|tcp|character|connection|unexpected|network|timeout|WSARecv|Connect|GetAddr|no such|reset|http|received|EOF|reused");
    }
    // 重定义需要容错的函数
    var names = ApiList.split(',');
    _.each(exchanges, function(e) {
        _.each(names, function(name) {
            if (typeof(e[name]) !== 'function') {
                throw "尝试容错 " + name + " 失败, 请确认存在此API并且输入正确.";
            }
            var old = e[name];
            e[name] = function() {
                var r;
                while (!(r = old.apply(this, Array.prototype.slice.call(arguments)))) {
                    if (Debug) {
                        Log(e.GetLabel(), name, "调用失败", RetryInterval, "毫秒后重试...");
                    }
                    Sleep(RetryInterval);
                }
                return r;
            };
        });
    });
    Log("容错机制开启", names);
}

// Test
function main() {
    // 此时GetTicker就不需要重试了
    Log(exchange.GetTicker());
}
```

> Detail

https://www.fmz.com/strategy/11609

> Last Modified

2016-04-03 17:17:41
