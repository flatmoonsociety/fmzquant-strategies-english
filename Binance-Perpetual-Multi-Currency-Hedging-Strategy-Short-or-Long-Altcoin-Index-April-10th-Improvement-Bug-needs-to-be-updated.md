
> Name

Binance Perpetual Multi-Currency Hedging Strategy Short or Long Altcoin Index April 10th Improvement Bug needs to be updated
> Author

grass
> Strategy Description

## **Important content! ! **
- Be sure to read this study https://www.fmz.com/digest-topic/5294 first. Understand the strategy principles, risks, how to screen trading pairs, how to set parameters, the ratio of opening positions to total funds, and a series of other issues.
- The previous research report needs to be downloaded and uploaded to your own research environment. Run the actual modifications. If you've seen this report, it was recently updated with data for the latest week.
- **The strategy cannot be backtested directly and needs to be backtested in a research environment**.
- The strategy code and default parameters are for research only. You need to be cautious when running real trading. Decide parameters based on your own research. **At your own risk**.
- **The strategy cannot be profitable every day. You can look at the backtest history. Sideways and retracements in 1-2 weeks are normal, and the backtest may be large, so you need to treat it correctly**
- The code is public and can be modified by yourself. If you have any questions, please leave comments and feedback. It is best to join the inventor Binance exchange group (how to join is in the research report) to get update notifications.
- **The strategy needs to run in full position mode. Do not set two-way positions. The strategy only supports Binance futures. When creating the robot, just use the default trading pair and K-line cycle. The strategy does not use K-line**
- **Strategies conflict with other strategies and manual operations and need to be noted**
- Real-time operation requires an overseas host. During the test phase, you can rent an Alibaba Cloud Hong Kong server with one click on the platform. It is cheaper to rent the entire server by yourself on a monthly basis (the lowest configuration is enough, deployment tutorial: https://www.fmz.com/bbs-topic/2848 )
- Binance’s futures and spot need to be added separately. Binance futures is ``Futures_Binance``
## Strategy Principle
The strategy will diversify into shorting a selected basket of altcoins at equal value, while simultaneously taking long positions on Bitcoin to hedge, reducing risk and volatility. As prices fluctuate, positions are constantly adjusted to keep the value of short positions constant and long positions equal. **Essentially shorting the Altcoin-Bitcoin Price Index**. The performance of the past two months (about 3 times leverage, data updated to 4.8), in the past week, altcoins have risen relative to Bitcoin, so they have suffered losses. If you are bullish on altcoins, you can set short Bitcoin and long altcoins in the parameters:
**The default strategy is long Bitcoin and short altcoins, you can also do the opposite (if you think altcoins are at the bottom), the decision is yours**
 ![IMG](https://www.fmz.com/upload/asset/24281c6de45544ca2b7.png) 



## Strategy logic
1. Update market conditions and account positions
2. Update the short position value of each altcoin and determine whether the short position needs to be adjusted.
3. Update the total short positions, determine the long positions, and determine whether the long positions need to be adjusted.
4. Place an order. The order quantity is determined by Bingshan Commission, and the transaction is completed according to the opponent's price (buy at the same price as the sell). **Cancel the order immediately after placing it (so you will see many orders with failed cancellation 400: {"code":-2011,"msg":"Unknown order sent."}, which is normal)**
5. Cycle again
** It will determine which trading pair has more Short_symbols and Long_symbols. The opening value of each currency with more is Trade_value, and the contract value of each currency with less is the average value that needs to be hedged. **
If you are only short BTC and long TRX, DASH, ONT, QTUM, and the Trade_value is 50, then TRX, DASH, ONT, and QTUM are all long positions 50, and BTC is short 50\*4.
If you are only long BTC and short TRX, DASH, ONT, QTUM, and the Trade_value is 50, then TRX, DASH, ONT, and QTUM all have short positions of 50, and BTC has long positions of 50\*4.
The leverage in the status bar represents the proportion of the margin that has been used, and should not be too high.
## Strategy parameters
 ![IMG](https://www.fmz.com/upload/asset/2c9e5e0e4c30f9eaada.png)  

- Short_symbols: Short-selling currencies, separated by ","
- Long_symbols: For long currencies, you can also leave it short, without hedging, or directly go short.
- Trade_value: short holding value of a single currency. You also need to do long hedging, the total value = 2\*Trade_value\*number of short currencies. Generally, 3-5 times leverage is used, that is, total value = 3*account balance. You need to decide based on the total amount of funds you invest. You can check the size of the leverage through backtesting in the research environment.
- Adjust_value: The contract value (priced in USDT) adjusts the deviation value. If it is too large, the adjustment will be slow, and if it is too small, the handling fee will be too high. It is decided based on Trade_value. It cannot be lower than 20, otherwise the minimum transaction will not be reached.
- Ice_value: Iceberg commission value, which cannot be less than 20. When placing an order, choose the smaller one between Adjust_value and Ice_value.

## Strategy Risk
When the price of the shorted currency rises and the contract value increases, the position is reduced. On the contrary, the profit is increased. This keeps the total contract value constant. It is very likely that altcoins will emerge from an independent market. From the current one-year cycle, altcoins may be at the bottom and may rise a lot from the bottom. It depends on how to use it. If you are optimistic about the altcoin and think it has reached the bottom, you can operate in the direction and go long on the index. Or if you are optimistic about certain currencies (not necessarily Bitcoin), you can hedge against them.

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Short_symbols|TRX,DASH,ONT,QTUM,BAT,IOST,ADA,ZEC,XMR,NEO,VET,XRP,IOTA,XLM|Short trading pairs|
|Long_symbols|BTC|Long trading pair|
|Trade_value|50|Single contract value for shorting|
|Adjust_value|20|Contract value adjustment deviation value|
|Ice_value|50|Size of iceberg order|
|Log_profit_interval|20|Log total equity interval s|
|Interval|5|Sleep time s|

> Source (javascript)

``` javascript
if(IsVirtual()){
    throw '不能回测，回测参考 https://www.fmz.com/digest-topic/5294 '
}
if(exchange.GetName() != 'Futures_Binance'){
    throw '只支持币安期货交易所，和现货交易所不同，需要单独添加，名称为Futures_Binance'
}

var short_symbols = Short_symbols.split(',')
var long_symbols = Long_symbols.split(',')

if(short_symbols.length == 1 && short_symbols[0] == ''){
    short_symbols = []
}
if(long_symbols.length == 1 && long_symbols[0] == ''){
    long_symbols = []
}
var symbols = []
for(var i=0; i<short_symbols.length; i++){
    if(short_symbols[i]){
        symbols.push(short_symbols[i])
    }
}
for(var i=0; i<long_symbols.length; i++){
    if(long_symbols[i]){
        symbols.push(long_symbols[i])
    }
}
var update_profit_time = 0
var assets = {}
var trade_info = {}
var exchange_info = HttpQuery('https://fapi.binance.com/fapi/v1/exchangeInfo')
if(!exchange_info){
    throw '无法连接币安网络，需要海外托管者'
}
exchange_info = JSON.parse(exchange_info)
for (var i=0; i<exchange_info.symbols.length; i++){
    if(symbols.indexOf(exchange_info.symbols[i].baseAsset) > -1){
       assets[exchange_info.symbols[i].baseAsset] = {amount:0, hold_price:0, value:0, bid_price:0, ask_price:0, realised_profit:0, margin:0, unrealised_profit:0}
       trade_info[exchange_info.symbols[i].baseAsset] = {minQty:parseFloat(exchange_info.symbols[i].filters[1].minQty),
                                                         priceSize:parseInt((Math.log10(1.1/parseFloat(exchange_info.symbols[i].filters[0].tickSize)))),
                                                         amountSize:parseInt((Math.log10(1.1/parseFloat(exchange_info.symbols[i].filters[1].stepSize))))
                                                        }
    }
}
assets.USDT = {unrealised_profit:0, margin:0, margin_balance:0, total_balance:0, leverage:0}


function updateAccount(){
    var account = exchange.GetAccount()
    var pos = exchange.GetPosition()
    if (account == null || pos == null ){
        Log('update account time out')
        return
    }
    assets.USDT.update_time = Date.now()
    for(var i=0; i<symbols.length; i++){
        assets[symbols[i]].margin = 0
        assets[symbols[i]].unrealised_profit = 0
        assets[symbols[i]].hold_price = 0
        assets[symbols[i]].amount = 0
        assets[symbols[i]].unrealised_profit = 0
    }
    for(var j=0; j<account.Info.positions.length; j++){
        if(account.Info.positions[j].positionSide == 'BOTH'){
            var pair = account.Info.positions[j].symbol 
            var coin = pair.slice(0,pair.length-4)
            if(symbols.indexOf(coin) < 0){continue}
            assets[coin].margin = parseFloat(account.Info.positions[j].initialMargin) + parseFloat(account.Info.positions[j].maintMargin)
            assets[coin].unrealised_profit = parseFloat(account.Info.positions[j].unrealizedProfit)
        }
    }
    assets.USDT.margin = _N(parseFloat(account.Info.totalInitialMargin) + parseFloat(account.Info.totalMaintMargin),2)
    assets.USDT.margin_balance = _N(parseFloat(account.Info.totalMarginBalance),2)
    assets.USDT.total_balance = _N(parseFloat(account.Info.totalWalletBalance),2)
    assets.USDT.unrealised_profit = _N(parseFloat(account.Info.totalUnrealizedProfit),2)
    assets.USDT.leverage = _N(assets.USDT.margin/assets.USDT.total_balance,2)
    pos = JSON.parse(exchange.GetRawJSON())
    if(pos.length > 0){
        for(var k=0; k<pos.length; k++){
            var pair = pos[k].symbol
            var coin = pair.slice(0,pair.length-4)
            if(symbols.indexOf(coin) < 0){continue}
            assets[coin].hold_price = parseFloat(pos[k].entryPrice)
            assets[coin].amount = parseFloat(pos[k].positionAmt)
            assets[coin].unrealised_profit = parseFloat(pos[k].unRealizedProfit)
        }
    }
}

function updateTick(){
    var ticker = HttpQuery('https://fapi.binance.com/fapi/v1/ticker/bookTicker')
    if(ticker == null){
        Log('get ticker time out')
        return
    }
    ticker = JSON.parse(ticker)
    for(var i=0; i<ticker.length; i++){
        var pair = ticker[i].symbol 
        var coin = pair.slice(0,pair.length-4)
        if(symbols.indexOf(coin) < 0){continue}
        assets[coin].ask_price = parseFloat(ticker[i].askPrice)
        assets[coin].bid_price = parseFloat(ticker[i].bidPrice)
        assets[coin].ask_value = _N(assets[coin].amount*assets[coin].ask_price, 2)
        assets[coin].bid_value = _N(assets[coin].amount*assets[coin].bid_price, 2)
    }
}

function trade(symbol, dirction, value){
    if(Date.now()-assets.USDT.update_time > 10*1000){
        Log('更新账户延时，不交易')
        return
    }
    var price = dirction == 'sell' ? assets[symbol].bid_price : assets[symbol].ask_price
    var amount = _N(Math.min(value,Ice_value)/price, trade_info[symbol].amountSize)
    if(amount < trade_info[symbol].minQty){
        Log(symbol, '合约调整偏离价值或冰山委托订单设置过小，达不到最小成交, 至少需要: ', _N(trade_info[symbol].minQty*price,0))
        return
    }
    exchange.IO("currency", symbol+'_'+'USDT')
    exchange.SetContractType('swap')
    exchange.SetDirection(dirction)
    var f = dirction == 'buy' ? 'Buy' : 'Sell'
    var id = exchange[f](price, amount, symbol)
    if(id){
        exchange.CancelOrder(id) //订单会立即撤销
    }
}



function updateStatus(){
        var table = {type: 'table', title: '交易对信息', 
             cols: ['币种', '数量', '持仓价格', '当前价格', '持仓价值', '保证金', '未实现盈亏'],
             rows: []}
    for (var i=0; i<symbols.length; i++){
        var price = _N((assets[symbols[i]].ask_price + assets[symbols[i]].bid_price)/2, trade_info[symbols[i]].priceSize)
        var value = _N((assets[symbols[i]].ask_value + assets[symbols[i]].bid_value)/2, 2)
        var infoList = [symbols[i], assets[symbols[i]].amount, assets[symbols[i]].hold_price, price, value,_N(assets[symbols[i]].margin,3), _N(assets[symbols[i]].unrealised_profit,3)]
        table.rows.push(infoList)
    }
    var logString = _D() + '  ' + JSON.stringify(assets.USDT) + '\n'
    LogStatus(logString + '`' + JSON.stringify(table) + '`')
    
    if(Date.now()-update_profit_time > Log_profit_interval*1000){
        LogProfit(_N(assets.USDT.margin_balance,3))
        update_profit_time = Date.now()
    }
    
}

function onTick(){
    var short_value = Trade_value
    if(short_symbols.length<long_symbols.length){
        short_value = _N(long_symbols.length*Trade_value/short_symbols.length,0)
    }
    var long_value = Trade_value
    if(short_symbols.length>long_symbols.length){
        long_value = _N(short_symbols.length*Trade_value/long_symbols.length,0)
    }
    var symbol = ''
    for(var i=0; i<short_symbols.length; i++){
        symbol = short_symbols[i]
        if(assets[symbol].ask_price == 0){ continue }
        if(assets[symbol].bid_value + short_value > Adjust_value){
            trade(symbol, 'sell', assets[symbol].bid_value + short_value)
        }
        if(assets[symbol].ask_value + short_value < -Adjust_value){
            trade(symbol, 'buy', -(assets[symbol].ask_value + short_value))
        }
    }
    for(var i=0; i<long_symbols.length; i++){
        symbol = long_symbols[i]
        if(assets[symbol].ask_price == 0){ continue }
        if(assets[symbol].bid_value - long_value > Adjust_value){
            trade(symbol, 'sell', assets[symbol].bid_value-long_value)
        }
        if(assets[symbol].ask_value - long_value < -Adjust_value){
            trade(symbol, 'buy', long_value-assets[symbol].ask_value)
        }
    }   
}

function main() {
    while(true){
        updateAccount()
        updateTick()
        onTick()
        updateStatus()
        Sleep(Interval*1000)
    }
}
```

> Detail

https://www.fmz.com/strategy/194825

> Last Modified

2020-08-04 14:22:07
