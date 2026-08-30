
> Name

Get the full currency name of Binance usdt contract
> Author

Xin
> Strategy Description

1. Put in the FMZ debugging tool and run it directly.
2. Get the name and number of all currencies of Binance usdt contract


> Source (javascript)

``` javascript
function unique (str) {
	var arr = str.split(',');
	return Array.from(new Set(arr)).join(',')
}

function main() {
    var exchange_info = JSON.parse(HttpQuery('https://fapi.binance.com/fapi/v1/exchangeInfo'));
    var str = '';
    exchange_info.symbols.forEach(function(exitem, index) {
        if (exitem.symbol.indexOf('USDT') == -1) {return}
        if (exitem.symbol.indexOf('BTCST') !== -1) {return}
        if (exitem.symbol.indexOf('BTCDOM') !== -1) {return}
        var content = ',';
        if (index == exchange_info.symbols.length - 1) {
            content = '';
        }
        str += exitem.baseAsset + content;
    });
	Log('全合约币种数量：', unique(str).split(',').length)
    Log('全合约币种名称：',unique(str))
    // return leverageBracket;

    let leverageBracket = exchange.IO("api", "GET", "/fapi/v1/leverageBracket", "timestamp=" + new Date().getTime())
    let newList = leverageBracket.map((item) => {
        return {
            symbol: item.symbol,
            leverage: item.brackets[0].initialLeverage
        }
    })
    let selectLeverage = 25;
    newList = newList.filter((item) => {
        return item.leverage >= selectLeverage;
    })
    Log('筛选币数量：' , newList.length);
    let str2 = ''

    newList.forEach(function(exitem, index) {
        if (exitem.symbol.indexOf('USDT') == -1) {return}
        if (exitem.symbol.indexOf('BTCST') !== -1) {return}
        if (exitem.symbol.indexOf('BTCDOM') !== -1) {return}
        var content = ',';
        if (index == newList.length - 1) {
            content = '';
        }
        str2 += exitem.baseAsset + content;
    });
    Log('筛选币名称：', str);
}

```

> Detail

https://www.fmz.com/strategy/327743

> Last Modified

2023-09-26 20:50:01
