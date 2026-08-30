
> Name

Iceberg Commission-Sell
> Author

Zero

> Strategy Description

Iceberg orders mean that when investors conduct large-amount transactions, in order to avoid excessive impact on the market, the large orders are automatically split into multiple orders, and small orders are automatically made based on the current latest buy/sell price and the price strategy set by the customer. When the previous order is fully completed or the latest price deviates significantly from the current order price, the order is automatically re-entrusted.
Example:
If the number of single-time average floating points is set to 10, then:
The quantity of each order is 90% to 110% of the average value of a single order. The order price is the latest selling price 1 * (1 + order depth). A new order will be placed after the previous order is fully completed. When the latest transaction price is more than the order depth * 2 from the order, the order will be automatically canceled and the order will be re-entrusted. Stop placing orders when the strategy's total trading volume equals its total order quantity. The order is stopped when the latest transaction price of the market is lower than its lowest selling price, and the order is resumed after the latest transaction price is higher than the lowest selling price again.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|TotalSellStocks|10|Total quantity sold (coin)|
|AvgSellOnce|0.3|Average number of single sales (coin)|
|FloatPoint|10|Single average number of floating points (percentage)|
|EntrustDepth|0.1|Entrust depth (percentage)|
|MinSellPrice|3800|Minimum selling price (yuan)|
|Interval|1000|Failed retry (milliseconds)|
|MinStock|0.0001|Minimum trading volume|
|LoopInterval|300|Price polling interval (milliseconds)|

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

var LastSellPrice = 0;
var InitAccount = null;

function dispatch() {
    var account = null;
    var ticker = _C(exchange.GetTicker);
    // 在最新成交价格距离该笔委托超过委托深度*2时自动撤单并重新进行委托
    if (LastSellPrice > 0) {
        // 订单没有完成
        if (_C(exchange.GetOrders).length > 0) {
            if (ticker.Last < LastSellPrice && ((LastSellPrice - ticker.Last) / ticker.Last) > (2*(EntrustDepth/100))) {
                Log('偏离过多, 最新成交价:', ticker.Last, '委托价', LastSellPrice);
                CancelPendingOrders();
            } else {
                return true;
            }
        } else {
            account = _C(exchange.GetAccount);
            Log("卖单完成, 累计卖出:", _N(InitAccount.Stocks - account.Stocks), "平均卖出价:", _N((account.Balance - InitAccount.Balance) / (InitAccount.Stocks - account.Stocks))); }
            LastSellPrice = 0;
    }

    // 委托价格为最新卖1价*（1+委托深度）
    var SellPrice = _N(ticker.Sell * (1 + EntrustDepth/100));
    if (SellPrice < MinSellPrice) {
        return true;
    }

    if (!account) {
        account = _C(exchange.GetAccount);
    }


    if ((InitAccount.Stocks - account.Stocks) >= TotalSellStocks) {
        return false;
    }

    var RandomAvgSellOnce = (AvgSellOnce * ((100 - FloatPoint) / 100)) + (((FloatPoint * 2) / 100) * AvgSellOnce * Math.random());
    var SellAmount = Math.min(TotalSellStocks - (InitAccount.Stocks - account.Stocks), RandomAvgSellOnce);
    if (SellAmount < MinStock) {
        return false;
    }
    LastSellPrice = SellPrice;
    exchange.Sell(SellPrice, SellAmount, '上次成交价', ticker.Last);
    return true;
}

function main() {
    if (exchange.GetName().indexOf('Futures_') != -1) {
        throw "只支持现货";
    }
    CancelPendingOrders();
    InitAccount = _C(exchange.GetAccount);
    Log(InitAccount);
    if (InitAccount.Stocks < TotalSellStocks) {
        throw "账户币数不足";
    }
    LoopInterval = Math.max(LoopInterval, 1);
    while (dispatch()) {
        Sleep(LoopInterval);
    }
    Log("委托全部完成", _C(exchange.GetAccount));
}


```

> Detail

https://www.fmz.com/strategy/241

> Last Modified

2020-03-06 19:47:44
