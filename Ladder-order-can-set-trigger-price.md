
> Name

Ladder order-can set trigger price
> Author

Zero

> Strategy Description

Ladder orders can be bought or sold. The program places a specified number of buy orders or sell orders according to the order interval. If it is a buy order, the first order will be the highest priced order, and the prices of subsequent orders will decrease in sequence. The first sell order will be the cheapest sell order, and the subsequent prices will increase in sequence.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|OpType|0|Place a buy order: Buy order|Sell order|
|StartPrice|20|Initial price of order|
|PriceDiff|0.2|Order Interval|
|OrderNum|10|Number of orders placed|
|Amount|0.8|Amount of coins per order|
|EnableTrigger|false|Use trigger conditions|
|TriggerPrice|18|Trigger Price|

> Source (javascript)

``` javascript
function adjustFloat(v) {
    return Math.floor(parseFloat(v.toFixed(10))*1000)/1000;
}

function GetAccount(e) {
    var account;
    while (!(account = exchange.GetAccount())) {
        Sleep(Interval);
    }
    return account;
}

function GetTicker() {
    var ticker;
    while (!(ticker = exchange.GetTicker())) {
        Sleep(1000);
    }
    return ticker;
}

function main() {
    var ticker = GetTicker();
    var InitPrice = ticker.Last;
    if (EnableTrigger) {
        Log('当前价格: ', InitPrice, InitPrice > TriggerPrice ? '价格跌破' : '价格涨超', TriggerPrice, '时触发阶梯下单');
        while (true) {
            if (InitPrice > TriggerPrice && ticker.Last < TriggerPrice) {
                Log('当前价格', ticker.Last, '价格跌破 ', TriggerPrice, '元, 开始下单');
                break;
            } else if (InitPrice < TriggerPrice && ticker.Last > TriggerPrice) {
                Log('当前价格', ticker.Last, '价格涨超 ', TriggerPrice, '元, 开始下单');
                break;
            }
            ticker = GetTicker();
            Sleep(1000);
        }
    }
    var account = GetAccount();
    var needMoney = 0;
    var needStocks = 0;
    for (var i = 0; i < OrderNum; i++) {
        needMoney += (StartPrice - (i * PriceDiff)) * Amount;
        needStocks += Amount;
    }

    if (OpType == 0) {
        if (needMoney > account.Balance) {
            throw "没有足够的钱下单";
        }
        for (var i = 0; i < OrderNum; i++) {
            exchange.Buy(adjustFloat(StartPrice - (i * PriceDiff)), Amount);
        }
    } else {
        if (needStocks > account.Stocks) {
            throw "没有足够的币下单";
        }
        for (var i = 0; i < OrderNum; i++) {
            exchange.Sell(adjustFloat(StartPrice + (i * PriceDiff)), Amount);
        }        
    }
    Log("全部委托完成");
}
```

> Detail

https://www.fmz.com/strategy/639

> Last Modified

2015-04-22 16:18:14
