
> Name

Get K-line-0804 updates from third-party websites
> Author

Number · Crazy
> Strategy Description

For platforms that do not support obtaining K-line data (BitVC futures, BTCC's BTC spot, Chinese Bitcoin's ETH, ETC), if enough K-lines must be obtained at the beginning of the strategy, you can use this template to directly obtain the platform's historical K-line data from a third-party website.
Note:
K-line data is updated every 3 seconds, so it cannot be called frequently.
Applicable to real transactions only.
The author does not guarantee the accuracy of third-party data and the correctness of the program, it is for learning reference only.
Update 0427: The exceptions that may be thrown when Parse JSON data are processed, and the return value when an exception occurs is uniformly null.


> Source (javascript)

``` javascript

$.AltRecords = function(exchange, timeframe, size, includeLastBar) {
    var symbol;
    var info;
    var record = [];
    if (!size) size="";
    // 目前只支持以下三个交易所，其余交易所接口可参考https://www.btc123.com/api
    if (exchange.GetName().indexOf('Futures_BitVC') != -1) { 
        symbol = "bitvcbtccnyfuture";
    }
    else if (exchange.GetName().indexOf('BTCC') != -1 && exchange.GetCurrency().indexOf('BTC') != -1) {
        symbol = "btcchinabtccny";
    }
    else if (exchange.GetName().indexOf('CHBTC') != -1 && exchange.GetCurrency().indexOf('ETH') != -1) {
        symbol = "chbtcethcny";
    }
    else if (exchange.GetName().indexOf('CHBTC') != -1 && exchange.GetCurrency().indexOf('ETC') != -1) {
        symbol = "chbtcetccny";
    }
    
    if (symbol) {
        try {
            info = JSON.parse(HttpQuery('https://www.btc123.com/market/kline?symbol='+symbol+'&type='+timeframe+'&size='+(includeLastBar ? size : size+1)));
            if (info && info.isSuc) {
                info = JSON.parse(info.datas.data);
            }
            else {
                Log("获取K线时发生错误:", info && info.des ? info.des : "网络错误");
                return null;
            }
        } catch (e) {
            Log("获取K线时发生错误:", info && info.des ? info.des : "网络错误");
            return null;
        }
        for (var i = 0; i < (includeLastBar ? info.length : info.length-1); i++) {
            record.push({"Time": info[i][0], "Open": info[i][1], "High": info[i][2], "Low": info[i][3], "Close": info[i][4], "Volume": info[i][5]});
        }
        return record;
    }
    return exchange.GetRecords(); // 不支持的交易所采用默认方式处理（忽略所有参数，如时间周期、长度等）。
};

function main() {
    Log(exchange.GetName());
    var rec = $.AltRecords(exchange, "5min", 100); // 获取5分钟K线, 100条, 不含最后一条Bar
    if (rec) Log(rec.length, rec[rec.length-1]);
    rec = $.AltRecords(exchange, "4hour", 100, 1); // 获取4小时K线, 100条, 含最后一条Bar
    if (rec) Log(rec.length, rec[rec.length-1]);
}
```

> Detail

https://www.fmz.com/strategy/12977

> Last Modified

2016-08-04 22:35:27
