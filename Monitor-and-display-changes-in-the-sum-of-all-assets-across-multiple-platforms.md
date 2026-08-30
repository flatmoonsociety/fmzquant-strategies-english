
> Name

Monitor and display changes in the sum of all assets across multiple platforms
> Author

Zero

> Strategy Description

Monitor and display the total assets of multiple platforms. It will be re-displayed when the account funds change. The money and coins of all platforms will be converted into net assets and displayed on the income curve.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|1000|Failed retry (milliseconds)|
|TickInterval|5000|Monitoring frequency (milliseconds)|

> Source (javascript)

``` javascript
var LastState = null;

function adjustFloat(v) {
    return Math.floor(v*1000)/1000;
}

function getExchangesState() {
    var isUpdate = false;
    var allBalance = 0;
    var allNetStocks = 0;
    var Cache = [];
    var CurrencyCache = [];
    for (var i = 0; i < exchanges.length; i++) {
        var account = null;
        var ticker = null;
        while (!(account = exchanges[i].GetAccount())) {
            Sleep(Interval);
        }
        while (!(ticker = exchanges[i].GetTicker())) {
            Sleep(Interval);
        }        
        var name = typeof(exchanges[i].GetLabel) == 'undefined' ? exchanges[i].GetName() : exchanges[i].GetLabel();
        var currency = exchanges[i].GetCurrency();
        if (typeof(CurrencyCache[currency]) == 'undefined') {
            CurrencyCache[currency] = 0;
        }
        CurrencyCache[currency] = adjustFloat(CurrencyCache[currency] + account.Stocks + account.FrozenStocks);
        if (typeof(Cache[name]) == 'undefined') {
            Cache[name] = true;
            allBalance += account.Balance + account.FrozenBalance;
        }
        allNetStocks += (account.Stocks + account.FrozenStocks) * ticker.Last;
    }
    var update = false;
    var str = "";
    for (var currency in CurrencyCache) {
        str += ' '+currency + ': ' + CurrencyCache[currency];
        if (LastState != null) {
            if (LastState.CurrencyCache[currency] != CurrencyCache[currency]) {
                update = true;
            }
        }
    }
    allBalance = adjustFloat(allBalance);
    if (LastState != null) {
        if (LastState.allBalance != allBalance) {
            update = true;
        }
    }
    
    return {allStocks: str, Net: adjustFloat(allNetStocks + allBalance), CurrencyCache: CurrencyCache, allBalance: allBalance, update: (LastState == null) || update};
}

function main() {
    Log("所有平台的钱和币将换算成净资产显示到收益曲线里");
    while (true) {
        var state = getExchangesState();
        if (state.update) {
            LastState = state;
            Log('总钱: ', state.allBalance, '总币: ', state.allStocks);
            LogProfit(state.Net);
        }
        Sleep(Math.max(TickInterval, 100));
    }
}
```

> Detail

https://www.fmz.com/strategy/443

> Last Modified

2014-12-04 01:30:50
