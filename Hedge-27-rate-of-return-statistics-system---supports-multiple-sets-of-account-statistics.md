
> Name

Hedge 27 rate of return statistics system - supports multiple sets of account statistics
> Author

Zero

> Strategy Description

The hedging 2.7 yield statistics system supports multiple groups of account statistics. You can start statistics by adding exchanges with an even length. Every two are added as a group.
The currency price will be based on the first exchange’s bid price as a reference value.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|60|Statistical interval (seconds)|
|InitMode|0|Mode for counting initial funds: automatic statistics|manual input|
|InitBalance|false|Initial total money|
|InitStocks|false|Initial total coins|

> Source (javascript)

``` javascript
//

function main() {
    if (exchanges.length == 0 || exchanges.length % 2 !== 0) {
        throw "交易所参数必须是2的整数";
    }
    var cfg = {
        __isStock: true,
        tooltip: {
            xDateFormat: '%Y-%m-%d %H:%M:%S, %A'
        },
        title: {
            text: '多平台收益率统计'
        },
        subtitle: {
            text: '正在统计...'
        },
        xAxis: {
            type: 'datetime'
        },
        legend: {
            enabled: true,
        },
        rangeSelector: {
            buttons: [{
                type: 'hour',
                count: 1,
                text: '1h'
            }, {
                type: 'hour',
                count: 3,
                text: '3h'
            }, {
                type: 'hour',
                count: 8,
                text: '8h'
            }, {
                type: 'all',
                text: 'All'
            }],
            selected: 0,
            inputEnabled: false
        },
        series: []
    };
    var i = 0;
    for (i = 0; i < exchanges.length; i += 2) {
        cfg.series.push({
            name: exchanges[i].GetLabel() + '/' + exchanges[i + 1].GetLabel(),
            data: [],
            tooltip: {
                valueDecimals: 4
            }
        });
    }
    var chart = Chart(cfg);
    var counter = 0;
    var getAccounts = function() {
        var accounts = [];
        for (var i = 0; i < exchanges.length; i++) {
            accounts.push(_C(exchanges[i].GetAccount));
        }
        return accounts;
    };
    var initAccounts = getAccounts();
    if (InitMode == 1) {
        Log("初始总资金手动指定为, 钱: ", InitBalance, "币:", InitStocks);
    } else {
        InitBalance = 0;
        InitStocks = 0;
        for (var i = 0; i < initAccounts.length; i++) {
            InitBalance += initAccounts[i].Balance + initAccounts[i].FrozenBalance;
            InitStocks += initAccounts[i].Stocks + initAccounts[i].FrozenStocks;
        }
        Log("初始总资金自动指定为, 钱: ", InitBalance, "币:", InitStocks);
    }
    while (true) {
        if (counter > 0) {
            Sleep(Interval * 1000);
        }
        counter++;
        var tbl = {
            type: 'table',
            title: '账户信息',
            cols: ['交易所', '当前组收益', '初始钱', '初始币', '当前钱', '当前币'],
            rows: []
        };
        var ticker = _C(exchange.GetTicker);
        var accounts = getAccounts();
        var ts = new Date().getTime();
        var allBalance = 0;
        var allStocks = 0;
        for (i = 0; i < accounts.length; i += 2) {
            var profit = (accounts[i].Balance + accounts[i].FrozenBalance + accounts[i + 1].Balance + accounts[i + 1].FrozenBalance) - (initAccounts[i].Balance + initAccounts[i].FrozenBalance + initAccounts[i + 1].Balance + initAccounts[i + 1].FrozenBalance) + (((accounts[i].Stocks + accounts[i].FrozenStocks + accounts[i + 1].Stocks + accounts[i + 1].FrozenStocks) - (initAccounts[i].Stocks + initAccounts[i].FrozenStocks + initAccounts[i + 1].Stocks + initAccounts[i + 1].FrozenStocks)) * ticker.Buy);
            chart.add(i / 2, [ts, _N(profit)]);
            for (var j = i; j < (i+2); j++) {
                tbl.rows.push([exchanges[j].GetLabel(), j % 2 == 0 ? _N(profit, 4) : '--', initAccounts[j].Balance + (initAccounts[j].FrozenBalance > 0 ? ' ( 冻结: ' + initAccounts[j].FrozenBalance + ' )' : ''), initAccounts[j].Stocks+ (initAccounts[j].FrozenStocks > 0 ? ' ( 冻结: ' + initAccounts[j].FrozenStocks + ' )' : ''), accounts[j].Balance+ (accounts[j].FrozenBalance > 0 ? ' ( 冻结: ' + accounts[j].FrozenBalance + ' )' : ''), accounts[j].Stocks+ (accounts[j].FrozenStocks > 0 ? ' ( 冻结: ' + accounts[j].FrozenStocks + ' )' : '')]);
                allBalance += accounts[j].Balance + accounts[j].FrozenBalance;
                allStocks += accounts[j].Stocks + accounts[j].FrozenStocks;
            }
        }
        cfg.subtitle.text = "初始总钱: " + _N(InitBalance) + ", 初始总币: " + _N(InitStocks) + ", 当前总钱: " + _N(allBalance) + ", 当前总币: " + _N(allStocks) + ", 买一价: " + ticker.Last + ", 总利润: " + _N((allBalance-InitBalance) + ((allStocks-InitStocks) * ticker.Buy)) + " 元";
        chart.update(cfg);
        LogStatus('`' + JSON.stringify(tbl) + '`');
    }
}
```

> Detail

https://www.fmz.com/strategy/18678

> Last Modified

2016-08-13 18:32:22
