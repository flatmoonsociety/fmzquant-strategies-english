
> Name

OKCoin futures conditions trigger order with stop loss
> Author

Zero

> Strategy Description

OKCoin futures conditions trigger the order, and after the transaction is completed, the automatic stop loss can be triggered conditionally.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|CType|0|Currency type: RMB|USD|
|ContractType|0|Contract Type: Current Week|Next Week|Current Month|Quarter|
|OpType|0|Operation type: Open long|Open short|
|MLevel|0|Leverage size: 10x|20x|
|TriggerType|0|Trigger method: rising or falling|
|TriggerPrice|2000|Opening trigger price (yuan)|
|OrderPrice|2005|Opening order price (yuan)|
|OrderAmount|true|Opening order amount|
|StopLossTrigger|1800|Stop loss trigger price (yuan)|
|StopOrderPrice|1790|Stop order price (yuan)|
|LoopInterval|300|Polling interval (milliseconds)|

> Source (javascript)

``` javascript
var _ContractType = ["this_week", "next_week", "month", "quarter"][ContractType];
var _TradeType = ["buy", "sell"][OpType];
var _MarginLevel = [10, 20][MLevel];
var Interval = 300;

function GetTicker() {
    var ticker;
    while (!(ticker = exchange.GetTicker())) {
        Sleep(Interval);
    }
    return ticker;
}

function GetOrders() {
    var orders;
    while (!(orders = exchange.GetOrders())) {
        Sleep(Interval);
    }
    return orders;
}

function GetAccount(maxRetry) {
    var account;
    var counter = 0;
    while (!(account = exchange.GetAccount())) {
        Sleep(Interval);
        counter++;
        if (typeof(maxRetry) == 'number' && counter > maxRetry) {
            break;
        }
    }
    return account;
}

function now() {
    var t = new Date();
    var year = t.getFullYear();
    var month = t.getMonth() + 1;
    var day = t.getDate();
    var hour = t.getHours();
    var minute = t.getMinutes();
    var second = t.getSeconds();

    if (month < 10) {
        month = '0' + month;
    }
    if (day < 10) {
        day = '0' + day;
    }
    if (hour < 10) {
        hour = '0' + hour;
    }
    if (minute < 10) {
        minute = '0' + minute;
    }
    if (second < 10) {
        second = '0' + second;
    }

    return year + '-' + month + '-' + day + ' ' + hour + ':' + minute + ':' + second;
}

function main() {
    if (exchange.GetName() != 'Futures_OKCoin') {
        throw "该策略为OKCoin期货专用策略";
    }
    if (CType == 1) {
        exchange.SetRate(1);
    }
    Log(CType == 0 ? "货币为RMB" : "货币为美元...");
    
    var account = GetAccount(10);
    if (!account) {
        throw "获取账户信息失败, 请检测API配置是否正确, 只支持逐仓模式";
    }

    SetErrorFilter("502:|503:|network|timeout|WSARecv|Connect|GetAddr|no such|reset");
    Log(account);
    Log('当前机器人ID: ', _G(), '开始运行...');
    
    exchange.SetContractType(_ContractType);
    exchange.SetMarginLevel(_MarginLevel);

    LoopInterval = Math.max(LoopInterval, 100);

    var ticker = GetTicker();
    var preLast = 0;
    Log('当前价格:', ticker.Last, '等待价格', TriggerType == 0 ? '涨超' : '跌破', TriggerPrice, '元...');
    while (true) {
        if (TriggerType == 1 && ticker.Last < TriggerPrice) {
            Log('价格跌破 ', TriggerPrice, '元, 开始按计划委托');
            break;
        } else if (TriggerType == 0 && ticker.Last > TriggerPrice) {
            Log('价格涨超 ', TriggerPrice, '元, 开始按计划委托');
            break;
        }
        ticker = GetTicker();
        if (ticker.Last != preLast) {
            preLast = ticker.Last;
            LogStatus("最新成交价: ", ticker.Last, now());
        }
        Sleep(LoopInterval);
    }
    Log("最后成交价: ", ticker.Last);
    exchange.SetDirection(_TradeType);
    var pfn = _TradeType == "buy" ? exchange.Buy : exchange.Sell;
    var orderId = pfn(OrderPrice, OrderAmount);
    if (!orderId) {
        Log("第一次下单失败, 重试最后一次!");
        orderId = pfn(OrderPrice, OrderAmount);
    }

    if (!orderId) {
        throw "下单失败";
    }
    Log("开始等待订单完成, 订单号:", orderId);
    while (true) {
        var order = exchange.GetOrder(orderId);
        if (order && order.Status == ORDER_STATE_CLOSED) {
            break;
        }
        Sleep(LoopInterval);
    }
    Log("订单完成, 开始等待止损...");

    var ticker = GetTicker();
    Log('当前价格:', ticker.Last, '止损条件:', _TradeType == "buy" ? '跌破' : '涨超', StopLossTrigger, '元');
    while (true) {
        if (_TradeType == "buy" && ticker.Last <= StopLossTrigger) {
            Log('价格跌破 ', StopLossTrigger, '元, 开始止损.');
            break;
        } else if (_TradeType == "sell" && ticker.Last >= StopLossTrigger) {
            Log('价格涨超 ', StopLossTrigger, '元, 开始止损.');
            break;
        }
        ticker = GetTicker();
        if (ticker.Last != preLast) {
            preLast = ticker.Last;
            LogStatus("最新成交价: ", ticker.Last, now());
        }
        Sleep(LoopInterval);
    }
    for (var i = 0; i < 2; i++) {
        if (_TradeType == "buy") {
            exchange.SetDirection("closebuy");
            orderId = exchange.Sell(StopOrderPrice, OrderAmount);
        } else {
            exchange.SetDirection("closesell");
            orderId = exchange.Buy(StopOrderPrice, OrderAmount);
        }
        if (orderId) {
            break;
        }
    }
    Log("完成所有操作, 策略退出.");
}
```

> Detail

https://www.fmz.com/strategy/2169

> Last Modified

2014-12-10 15:33:25
