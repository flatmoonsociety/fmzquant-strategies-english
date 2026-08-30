
> Name

Digital currency futures double moving average turning point strategy teaching
> Author

Inventor Quantification-Little Dream
> Strategy Description

Related articles: https://www.fmz.com/bbs-topic/8479
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|ema1Period|The period of the first EMA moving average indicator|EMA1 moving average period|
|ema2Period|The period of the second EMA moving average indicator|EMA2 moving average period|
|amount|Binance can be a decimal, and the contract order amount on most futures exchanges is the number of contracts (integer) |Contract order amount|
|profitTarget|Take profit difference, fill in 20 and earn 20 price difference. Take profit and close the position|Take profit|
|ct|Perpetual contract is: swap, quarterly contract: quarter, for details, you can check the API document|Contract code|
|okexSimulate|Switch to OKEX V5 simulation disk|Switch to OKEX V5 simulation disk|

> Source (javascript)

``` javascript
/*backtest
start: 2021-09-01 00:00:00
end: 2021-12-02 00:00:00
period: 1h
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

var LONG = 1 
var SHORT = -1
var IDLE = 0

function getPosition(positions, direction) {
    var ret = {Price : 0, Amount : 0, Type : ""}
    _.each(positions, function(pos) {
        if (pos.Type == direction) {
            ret = pos
        }
    })
    return ret 
}

function cancellAll() {
    while (true) {
        var orders = _C(exchange.GetOrders)
        if (orders.length == 0) {
            break
        } else {
            for (var i = 0 ; i < orders.length ; i++) {
                exchange.CancelOrder(orders[i].Id, orders[i])
                Sleep(500)
            }
        }
        Sleep(500)
    }
}

function cover(tradeFunc, direction) {
    var mapDirection = {"closebuy": PD_LONG, "closesell": PD_SHORT}
    var positions = _C(exchange.GetPosition)
    var pos = getPosition(positions, mapDirection[direction])
    if (pos.Amount > 0) {
        cancellAll()
        exchange.SetDirection(direction)
        if (tradeFunc(-1, pos.Amount)) {
            return true 
        } else {
            return false 
        }
    }
    return true 
}

function main() {
    if (okexSimulate) {
        exchange.IO("simulate", true) // 切换到OKEX V5模拟盘测试 
        Log("切换到OKEX V5模拟盘")
    }    
    exchange.SetContractType(ct)
    var state = IDLE
    var holdPrice = 0
    var preTime = 0

    while (true) {
        var r = _C(exchange.GetRecords)
        var l = r.length
        if (l < Math.max(ema1Period, ema2Period)) {
            Sleep(1000)
            continue
        }
        var ema1 = TA.EMA(r, ema1Period)
        var ema2 = TA.EMA(r, ema2Period)
        
        // 画图
        $.PlotRecords(r, 'K线')
        if(preTime !== r[l - 1].Time){
            $.PlotLine('ema1', ema1[l - 2], r[l - 2].Time)
            $.PlotLine('ema2', ema2[l - 2], r[l - 2].Time)
            
            $.PlotLine('ema1', ema1[l - 1], r[l - 1].Time)
            $.PlotLine('ema2', ema2[l - 1], r[l - 1].Time)
            preTime = r[l - 1].Time
        } else {
            $.PlotLine('ema1', ema1[l - 1], r[l - 1].Time)
            $.PlotLine('ema2', ema2[l - 1], r[l - 1].Time)
        }
        
        var up = (ema1[l - 2] > ema1[l - 3] && ema1[l - 4] > ema1[l - 3]) && (ema2[l - 2] > ema2[l - 3] && ema2[l - 4] > ema2[l - 3])
        var down = (ema1[l - 2] < ema1[l - 3] && ema1[l - 4] < ema1[l - 3]) && (ema2[l - 2] < ema2[l - 3] && ema2[l - 4] < ema2[l - 3])
        if (up && (state == SHORT || state == IDLE)) {
            if (state == SHORT && cover(exchange.Buy, "closesell")) {
                state = IDLE
                holdPrice = 0
                $.PlotFlag(r[l - 1].Time, 'coverShort', 'CS')
            }
            exchange.SetDirection("buy")
            if (exchange.Buy(-1, amount)) {
                state = LONG
                holdPrice = r[l - 1].Close
                $.PlotFlag(r[l - 1].Time, 'openLong', 'L')
            }
        } else if (down && (state == LONG || state == IDLE)) {
            if (state == LONG && cover(exchange.Sell, "closebuy")) {
                state = IDLE
                holdPrice = 0
                $.PlotFlag(r[l - 1].Time, 'coverLong', 'CL')
            }
            exchange.SetDirection("sell")
            if (exchange.Sell(-1, amount)) {
                state = SHORT
                holdPrice = r[l - 1].Close
                $.PlotFlag(r[l - 1].Time, 'openShort', 'S')
            }
        }
        
        // 止盈
        if (state == LONG && r[l - 1].Close - holdPrice > profitTarget && cover(exchange.Sell, "closebuy")) {            
            state = IDLE
            holdPrice = 0
            $.PlotFlag(r[l - 1].Time, 'coverLong', 'CL')
        } else if (state == SHORT && holdPrice - r[l - 1].Close > profitTarget && cover(exchange.Buy, "closesell")) {            
            state = IDLE
            holdPrice = 0
            $.PlotFlag(r[l - 1].Time, 'coverShort', 'CS')
        }
        LogStatus(_D())
        Sleep(500)        
    }
}
```

> Detail

https://www.fmz.com/strategy/333269

> Last Modified

2025-02-18 17:34:56
