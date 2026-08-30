
> Name

Iceberg Commission-Buy
> Author

Zero

> Strategy Description

Iceberg orders mean that when investors conduct large-amount transactions, in order to avoid excessive impact on the market, the large orders are automatically split into multiple orders, and small orders are automatically made based on the current latest buy/sell price and the price strategy set by the customer. When the previous order is fully completed or the latest price deviates significantly from the current order price, the order is automatically re-entrusted.
Example:
If the number of single-time average floating points is set to 10, then:
The quantity of each order is 90% to 110% of the average value of a single order, and the order price is the latest buying price * (1 - order depth). A new order will be placed after all the previous orders are completed. When the latest transaction price is more than the order depth * 2 from the order, the order will be automatically canceled and the order will be re-entrusted. Stop placing orders when the strategy's total trading volume equals its total order quantity. The order is stopped when the latest transaction price of the market is higher than the highest bid price, and the order is resumed after the latest transaction price is lower than the highest bid price again.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|TotalBuyNet|10000|Total purchase amount (yuan)|
|AvgBuyOnce|100|Average single purchase quantity (yuan)|
|FloatPoint|10|Single average number of floating points (percentage)|
|EntrustDepth|0.1|Entrust depth (percentage)|
|MaxBuyPrice|20000|Maximum buying price (yuan)|
|Interval|1000|Failed retry (milliseconds)|
|MinStock|0.0001|Minimum trading volume|
|LoopInterval|true|Price polling interval (seconds)|

> Source (javascript)

``` javascript


function CancelPendingOrders() {
    while (true) {
        var orders = _C(exchange.GetOrders);
        if (orders.length == 0) {
            return;
        }

        for (var j = 0; j < orders.length; j++) {
            exchange.CancelOrder(orders[j].Id);
            if (j < (orders.length-1)) {
                Sleep(Interval);
            }
        }
    }
}

var LastBuyPrice = 0;
var InitAccount = null;

function dispatch() {
    var account = null;
    var ticker = _C(exchange.GetTicker);
    // 在最新成交价格距离该笔委托超过委托深度*2时自动撤单并重新进行委托
    if (LastBuyPrice > 0) {
        // 订单没有完成
        if (_C(exchange.GetOrders).length > 0) {
            if (ticker.Last > LastBuyPrice && ((ticker.Last - LastBuyPrice) / LastBuyPrice) > (2*(EntrustDepth/100))) {
                Log('偏离过多, 最新成交价:', ticker.Last, '委托价', LastBuyPrice);
                CancelPendingOrders();
            } else {
                return true;
            }
        } else {
            account = _C(exchange.GetAccount);
            Log("买单完成, 累计花费:", _N(InitAccount.Balance - account.Balance), "平均买入价:", _N((InitAccount.Balance - account.Balance) / (account.Stocks - InitAccount.Stocks)));
        }
        LastBuyPrice = 0;
    }
    
    
    // 委托价格为最新买1价*（1-委托深度）
    var BuyPrice = _N(ticker.Buy * (1 - EntrustDepth/100));
    if (BuyPrice > MaxBuyPrice) {
        return true;
    }
    
    if (!account) {
        account = _C(exchange.GetAccount);
    }


    if ((InitAccount.Balance - account.Balance) >= TotalBuyNet) {
        return false;
    }
    
    var RandomAvgBuyOnce = (AvgBuyOnce * ((100 - FloatPoint) / 100)) + (((FloatPoint * 2) / 100) * AvgBuyOnce * Math.random());
    var UsedMoney = Math.min(account.Balance, RandomAvgBuyOnce, TotalBuyNet - (InitAccount.Balance - account.Balance));
    
    var BuyAmount = _N(UsedMoney / BuyPrice);
    if (BuyAmount < MinStock) {
        return false;
    }
    LastBuyPrice = BuyPrice;
    exchange.Buy(BuyPrice, BuyAmount, '花费: ', _N(UsedMoney), '上次成交价', ticker.Last);
    return true;
}

function main() {
    if (exchange.GetName().indexOf('Futures_') != -1) {
        throw "只支持现货";
    }
    CancelPendingOrders();
    InitAccount = _C(exchange.GetAccount);
    Log(InitAccount);
    if (InitAccount.Balance < TotalBuyNet) {
        throw "账户余额不足";
    }
    LoopInterval = Math.max(LoopInterval, 1);
    while (dispatch()) {
        Sleep(LoopInterval * 1000);
    }
    Log("委托全部完成", _C(exchange.GetAccount));
}

```

> Detail

https://www.fmz.com/strategy/236

> Last Modified

2020-03-08 12:21:25
