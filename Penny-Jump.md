
> Name

High-frequency trading strategy-Penny-Jump
> Author

Zero

> Strategy Description

Today, suppose there is a stupid large institutional investor (mutual fund, bank, pension fund...). He wants to buy a stock, but does not want to buy it at the market price, so he places a large order to buy in the market. At this time, everyone in the market will see that someone has placed a large order in the limit order book and is ready to buy the stock.
Suppose the original order book of the market is 200 | $1.01 x $1.03 | 200, and then suddenly this stupid institutional investor comes in and places a buy order of 3,000 shares at $1.01. At this time, the order book will become 3,200 | $1.01 x $1.03 | 200. We usually call this stupid institutional investor an "elephant", and high-frequency traders know that the price of $1.01 has a supporting buy order, so they will increase their bid price by 1 cent to $1.02. This strategy is called Penny Jump. Because high-frequency traders know that there is an "elephant" supporting the next level. So if the price rises to $1.03 x $1.05, he can immediately earn a profit of $0.01.
If a high-frequency trader buys this stock, even if the price does not rise, because there is an elephant supporting it, he can quickly sell it back to the elephant at a price of $1.01.
For high-frequency traders, the way they make profits is actually very simple, which is to use the microstructure in the market to infer the intentions of their counterparties, and then establish positions before others do. Then make a small profit in a short period of time, and then quickly leave the market.
For this elephant, because he placed a huge buy order in the market, his trading intentions were exposed, and he naturally became the target of high-frequency traders.
In the real world of stock trading, there should be very few such stupid institutional investors who would blatantly place huge buy orders (or sell orders) on the market. On the contrary, what is common is that large institutional investors want to sell a stock, so they deliberately place huge buy orders to create an illusion to attract high-frequency traders to enter the market to push up the stock price, and then dump the stocks all at once. This is the intrigue in the trading world.
For high-frequency traders, once this strategy is seen through and "Gaming", they will come back to "Gaming" again and develop strategies to eat the tofu of this kind of "Gaming" by institutional investors.
Attached pictures:
https://dn-filebox.qbox.me/33ecc8cd888b2918dcfb4044913c3c89a4cd4061.jpg

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|2000|Error retry interval (milliseconds)|
|Lot|0.01|Lot size|
|DisableLog|false|Turn off order tracking|
|ElephantAmount|10|Elephant Level (BTC)|
|ElephantSpace|0.2|Elephant distance (yuan)|
|LockCount|true|Number of elephant confirmations|
|PennyTick|0.1|Jump|
|WaitInterval|5000|Buy order timeout (milliseconds)|
|CheckInterval|300|Quick check interval (milliseconds)|
|ProfitTick|5|Profit Tick|
|STTick|true|Stop-loss ticks|

> Source (javascript)

``` javascript

var Counter = {
    i: 0,
    w: 0,
    f: 0
};

// Variables
var InitAccount = null;

function CancelAll() {
    while (true) {
        var orders = _C(exchange.GetOrders);
        if (orders.length == 0) {
            break;
        }
        for (var i = 0; i < orders.length; i++) {
            exchange.CancelOrder(orders[i].Id);
        }
        Sleep(Interval);
    }
}

function updateStatus(msg) {
    LogStatus("调戏次数:", Counter.i, "成功:", Counter.w, "失败:", Counter.f, "\n"+msg+"#0000ff\n"+new Date());
}

function main() {
    if (DisableLog) {
        EnableLog(false);
    }
    CancelAll();
    InitAccount = _C(exchange.GetAccount);
    Log(InitAccount);
    var i = 0;
    var locks = 0;
    while (true) {
        Sleep(Interval);
        var depth = _C(exchange.GetDepth);
        if (depth.Asks.length === 0 || depth.Bids.length === 0) {
            continue;
        }
        updateStatus("搜索大象中.... 买一: " + depth.Bids[0].Price + ",  卖一:" + depth.Asks[0].Price + ", 锁定次数: " + locks);
        var askPrice = 0;
        for (i = 0; i < depth.Asks.length; i++) {
            if (depth.Asks[i].Amount >= Lot) {
                askPrice = depth.Asks[i].Price;
                break;
            }
        }
        if (askPrice === 0) {
            continue;
        }
        var elephant = null;
        // skip Bids[0]
        for (i = 1; i < depth.Bids.length; i++) {
            if ((askPrice - depth.Bids[i].Price) > ElephantSpace) {
                break;
            }
            if (depth.Bids[i].Amount >= ElephantAmount) {
                elephant = depth.Bids[i];
                break;
            }
        }

        if (!elephant) {
            locks = 0;
            continue;
        }
        locks++;
        if (locks < LockCount) {
            continue;
        }
        locks = 0;

        updateStatus("调戏大象中....大象在第" + i + "档, " + JSON.stringify(elephant));
        exchange.Buy(elephant.Price + PennyTick, Lot, "Bids[" + i + "]", elephant);
        var ts = new Date().getTime();
        while (true) {
            Sleep(CheckInterval);
            var orders = _C(exchange.GetOrders);
            if (orders.length == 0) {
                break;
            }
            if ((new Date().getTime() - ts) > WaitInterval) {
                for (var i = 0; i < orders.length; i++) {
                    exchange.CancelOrder(orders[i].Id);
                }
            }
        }
        var account = _C(exchange.GetAccount);
        var opAmount = _N(account.Stocks - InitAccount.Stocks);
        if (opAmount < 0.001) {
            Counter.f++;
            Counter.i++;
            continue;
        }
        updateStatus("买单得手: " + opAmount +", 开始出手...");
        exchange.Sell(elephant.Price + (PennyTick * ProfitTick), opAmount);
        var success = true;
        while (true) {
            var depth = _C(exchange.GetDepth);
            if (depth.Bids.length > 0 && depth.Bids[0].Price <= (elephant.Price-(STTick*PennyTick))) {
                success = false;
                updateStatus("没有得手, 开始止损, 当前买一: " + depth.Bids[0].Price);
                CancelAll();
                account = _C(exchange.GetAccount);
                var opAmount = _N(account.Stocks - InitAccount.Stocks);
                if (opAmount < 0.001) {
                    break;
                }
                exchange.Sell(depth.Bids[0].Price, opAmount);
            }
            var orders = _C(exchange.GetOrders);
            if (orders.length === 0) {
                break;
            }
            Sleep(CheckInterval);
        }
        if (success) {
            Counter.w++;
        } else {
            Counter.f++;
        }
        Counter.i++;
        var account = _C(exchange.GetAccount);
        LogProfit(account.Balance - InitAccount.Balance, account);
    }
}
```

> Detail

https://www.fmz.com/strategy/358

> Last Modified

2016-08-27 10:37:36
