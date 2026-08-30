
> Name

Get OK futures real-time price limit
> Author

Number · Crazy
> Strategy Description

Get the real-time price limit of OK futures, only firm orders are valid.
The code is for learning only. The author does not guarantee the correctness of the program, and you will be responsible for the consequences of trading based on it.


> Source (javascript)

``` javascript
$.GetLimit = function(currStr, contract) {
    var url = "https://www.okcoin.com/api/v1/future_price_limit.do?symbol=" + currStr + "_usd&contract_type=" + contract;
    var httpResp = HttpQuery(url);
    if (httpResp.indexOf("false") != -1) return null;
    var parsedResp;
    try {
        parsedResp = JSON.parse(httpResp);
    } catch (e) {
        return null;
    }
    return parsedResp;
};

function main() {
    var limit = $.GetLimit('btc', 'quarter'); // 获取 比特币 季度 合约限价
    Log(limit.high, limit.low); // 最高买入、最低卖出限价
    limit = $.GetLimit('ltc', 'this_week'); // 获取 莱特币 当周 合约限价
    Log(limit.high, limit.low); // 最高买入、最低卖出限价
    limit = $.GetLimit('btc', 'next_week'); // 获取 比特币 次周 合约限价
    Log(limit.high, limit.low); // 最高买入、最低卖出限价
    
}
```

> Detail

https://www.fmz.com/strategy/17028

> Last Modified

2016-06-19 11:15:05
