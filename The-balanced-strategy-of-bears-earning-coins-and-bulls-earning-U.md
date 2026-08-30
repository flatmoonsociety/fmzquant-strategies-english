
> Name

The balanced strategy of bears earning coins and bulls earning U
> Author

VIC

> Strategy Description

* The contract version of Buffett's concept of currency balance strategy, the default is to go long contracts with half position.
* Binance BUSD has no order handling fees, which can narrow the balance processing gap to the extreme and maximize profits and handling fee refunds.
* The principle and code are very simple. We learn from the writing methods of the big guys, and calculate the order point and lot number in advance to place the order. Theoretically, the larger the principal, the closer the rate of return is to the limit.
* It is not recommended to run if the price is less than 1000U. The limit of the minimum order value causes the gap between pending orders to be too large.
* The prerequisite for profit is that the currency price rises or fluctuates.
* Can be copied and directly backtested
* The capital capacity is large, but the disadvantage is that the market needs to be volatile or bullish slowly. In a long-term bear market, more long positions will be accumulated, but the position will not be liquidated.
*Finally, after trying Martin’s negative expectations and the high competition of high-frequency arbitrage, perhaps returning to value investing is the ultimate way to victory.
* Welcome to add me to VX with your avatar to communicate this strategy
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|pricePrecision|2|Price Precision|
|amountPrecision|3|Order precision|
|linjie|30|critical value|
|leverage|10|Initial leverage|

> Source (javascript)

``` javascript


/*backtest
start: 2019-12-01 00:00:00
end: 2024-02-07 23:59:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT","balance":100000}]
args: [["pricePrecision",2],["amountPrecision",3],["linjie",30]]
*/

function cancelAll() {
    while (1) {
        var orders = _C(exchange.GetOrders)
        if (orders.length == 0) {
            break
        }
        for (var i = 0; i < orders.length; i++) {
            exchange.CancelOrder(orders[i].Id, orders[i].Id)
            Sleep(100)
        }
        Sleep(100)
    }
}
function onexit() {
    //
    cancelAll()
}

function main() {
    exchange.SetContractType("swap")
    exchange.SetPrecision(pricePrecision, amountPrecision) //精度
    exchange.SetMarginLevel(leverage) //杠杆
    //LogProfitReset()
    LogReset(1)
    var buyOrderId
    var sellOrderId
    while (1) {
        var pos = _C(exchange.GetPosition)
        if (pos.length > 0) {
            var Mar = pos[0].Margin //保证金
        } else {
            var Mar = 0
        }

        var MarginLevel = leverage //杠杆
        var account = _C(exchange.GetAccount)
        var Bala = account.Balance //可用余额
        var Bal = Bala - Mar * (MarginLevel - 1) //去掉仓位的余额
        var ticker = _C(exchange.GetTicker)
        var price = ticker.Last //最新价
        var Qian = Mar + Bala
        LogStatus("币价：", price,"权益:",Qian)
        var orders = _C(exchange.GetOrders)
        if (orders.length == 0) { //没有订单
            if (Mar * MarginLevel - Bal > 2 * linjie) { //仓位价值多于余额 //临界价值
                exchange.SetDirection("closebuy")
                var Amount = 0.5 * (Mar * MarginLevel - Bal) / price
                exchange.Sell(-1, Amount)
            } else if (Bal - Mar * MarginLevel > 2 * linjie) { //余额多于仓位价值 //临界价值
                var Amount = 0.5 * (Bal - Mar * MarginLevel) / price
                exchange.SetDirection("buy")
                exchange.Buy(-1, Amount)
            } else {//状态平衡时双向挂单
                var Bprice = price * (Bal - linjie) / (Mar * leverage)
                var BAmount = 0.5 * linjie / Bprice
                exchange.SetDirection("buy")
                buyOrderId = exchange.Buy(Bprice, BAmount)
                var Sprice = price * (Bal - (-linjie)) / (Mar * leverage)
                var SAmount = 0.5 * linjie / Sprice
                exchange.SetDirection("closebuy")
                sellOrderId = exchange.Sell(Sprice, SAmount)
            }


        } else { //有订单
            var isFindBuyId = false
            var isFindSellId = false
            //Log("初始状态")
            for (var i = 0; i < orders.length; i++) {

                if (buyOrderId == orders[i].Id) {
                    isFindBuyId = true
                    //Log("有买单")
                }
                if (sellOrderId == orders[i].Id) {
                    isFindSellId = true
                    //Log("有卖单")
                }
            }
            if (!isFindBuyId || !isFindSellId) { //有一方成交,取消订单进入新循环
                cancelAll()
                var Qian = Mar + Bala
                LogProfit(Qian)
                //LogStatus("币价：", price)
            }

        }
        Sleep(5000)
    }
}
```

> Detail

https://www.fmz.com/strategy/339698

> Last Modified

2024-03-06 11:15:26
