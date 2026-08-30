
> Name

Binance multiple trading pairs-spot-used for market price liquidation
> Author

light cloud
> Strategy Description

This is used to clear the spot stock.
For example, if you run a spot grid or Martin strategy with multiple trading pairs, you don’t want to run away, but you have so many currencies in your hand that it would be too troublesome to sell them one by one.
Just use this, enter the currency into the parameters, and all the market prices will be automatically sold.
However, sometimes after selling out, there will still be assets with a valuation less than 0.0012 BTC. At this time, you need to use [Small Assets Exchange for BNB] in the spot wallet.
In other words, if you have BNB, it is best to sell it at the market price.
 ![IMG](https://www.fmz.com/upload/asset/59622a6123c4e006c00e.png) 
 
 ![IMG](https://www.fmz.com/upload/asset/5a004355bd61ce2b0d93.png) 
 
  ![IMG](https://www.fmz.com/upload/asset/5a3ccbbe2eb4ff9bee47.png) 

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|B_Sleep_time|5|Polling interval (seconds)|
|B_symbols|TRX_BUSD,LTC_BUSD,BCH_BUSD|Trading pairs|
|B_chongzhi|false|Reset|

> Source (javascript)

``` javascript
//全局变量
var arrSymbols = B_symbols.split(",") // 逗号分割交易品种字符串

//获取价格精度 数量精度 函数
function GetPrecision() {
    var precision = {
        price: 0, //精度-价格
        amount: 0 //精度-数量
    }
    var depth = _C(exchange.GetDepth)
    if (!depth) {
        throw '无法连接交易所行情,需要海外托管者'
    }
    for (var i = 0; i < depth.Asks.length; i++) {
        var amountPrecision = depth.Asks[i].Amount.toString().indexOf('.') > -1 ? depth.Asks[i].Amount.toString().split('.')[1].length : 0
        precision.amount = Math.max(precision.amount, amountPrecision) //数量精度
        var pricePrecision = depth.Asks[i].Price.toString().indexOf('.') > -1 ? depth.Asks[i].Price.toString().split('.')[1].length : 0
        precision.price = Math.max(precision.price, pricePrecision) //价格精度
    }
    return precision
}

//取消所有挂单函数
//形参e 是 exchange.SetCurrency()  的 exchange
function cancelAll(e) {
    while (true) {
        var orders = _C(e.GetOrders)
        if (orders.length == 0) {
            break
        } else {
            for (var i = 0; i < orders.length; i++) {
                e.CancelOrder(orders[i].Id, orders[i])
                Sleep(200)
            }
        }
        Sleep(200)
    }
}

function Trad() {
    for (var i = 0; i < arrSymbols.length; i++) {
        Sleep(500)
        symbol = arrSymbols[i]
        exchange.SetCurrency(symbol)
        var ticker = _C(exchange.GetTicker).Last //最新价
        var precision = GetPrecision() //获取数量精度、价格精度
        var acc = _C(exchange.GetAccount)
        var base_balance = acc.Stocks //币种 可用余额
        var base_FrozenStocks = acc.FrozenStocks //币种挂单冻结的数量
        var holdAmount = _N(parseFloat(base_balance + base_FrozenStocks), precision.amount) //持仓量 = 币种余额+冻结数量
        if (holdAmount == 0 || holdAmount * ticker < 10) { //没有持仓 就是一开始的状态，10USDT价值是币安现货的最小交易金额，小于10的没法交易
            cancelAll(exchange)
            Log(symbol, "没有持仓，或者持仓数量不足以交易，持仓数量：", holdAmount)
        }
        if (holdAmount * ticker >= 10) { //持仓价值 >= USDT价值，则有持仓。
            Log(symbol, "有持仓，持仓数量：", holdAmount, "市价清仓", "#B15BFF")
            cancelAll(exchange)
            Sleep(500)
            var clearsell = exchange.Sell(-1, holdAmount) //清仓
            Sleep(500)
            acc = _C(exchange.GetAccount)
            base_balance = acc.Stocks //币种 可用余额
            base_FrozenStocks = acc.FrozenStocks //币种挂单冻结的数量
            holdAmount = _N(parseFloat(base_balance + base_FrozenStocks), precision.amount) //重新获取持仓数量
            Log(symbol, "持仓数量：", holdAmount, "#B15BFF")
        }
    }
}

//退出撤销所有挂单 
function onexit() {
    Log("机器人停止，撤销所有挂单", "#6F00D2")
    for (var i = 0; i < arrSymbols.length; i++) {
        symbol = arrSymbols[i]
        exchange.SetCurrency(symbol)
        cancelAll(exchange)
        Sleep(200)
    }
    Sleep(200)
}

//出错退出撤销所有挂单
function onerror() {
    Log("机器人出错，撤销所有挂单", "#00BB00")
    for (var i = 0; i < arrSymbols.length; i++) {
        symbol = arrSymbols[i]
        exchange.SetCurrency(symbol)
        cancelAll(exchange)
        Sleep(200)
    }
    Sleep(200)
}

function main() {
    if (B_chongzhi) {
        // LogProfitReset() //清空收益图表，只清空图表，日志信息不清除
        LogReset() //清空日志。只清空日志，不清除图表。
        LogVacuum()
        Log("重置所有数据", "#FF0000")
    }
    while (true) {
        Trad()
        Sleep(B_Sleep_time * 1000)
    }
}


```

> Detail

https://www.fmz.com/strategy/360782

> Last Modified

2022-05-02 10:23:01
