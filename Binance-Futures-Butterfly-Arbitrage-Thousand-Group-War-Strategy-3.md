
> Name

Binance Futures Butterfly Arbitrage Thousand Group War Strategy 3
> Author

grass
> Strategy Description

Binance butterfly arbitrage strategy cannot be backtested. For specific principles, please refer to the library article: https://www.fmz.com/digest-topic/6102
**You need to read this strategy manual and do not run it without thinking. The strategy code is for reference only and can be modified as needed. Feedback is welcome. **
### Strategy Principles
Binance Coin-based contracts such as BTC and ETH have three contracts at the same time, namely perpetual BTCUSD_PERP, current quarter BTCUSD_200925, and second quarter BTCUSD_201225.
Perpetual contracts can be treated as spot prices. Generally, there are three price differences for hedging between two contracts: current quarter-perpetual, second quarter-perpetual, and second quarter-current quarter. Butterfly arbitrage requires the operation of three contracts, and the price difference is (second quarter-current quarter)-(current quarter-perpetual), that is, price difference = second quarter+perpetual-2\*current quarter. To go long on the spread, you need to open one long second-quarter and perpetual contract and short two current-quarter contracts.
### Strategy parameters
- Transaction currency: Three types of perpetual, current quarter, and second quarter must exist at the same time.
- Number of orders placed: the number of orders placed in each grid.
- Grid opening spread: for each spread deviation, one share will be long or short.
- Spread smoothing parameter Alpha: used to calculate the average of the spread, you can use the default, or you can backtest by yourself.
- Iceberg order number: If the number of open positions is too large, in order to reduce the single-leg phenomenon, you can set the minimum number of orders for each opening. The disadvantage is that it is not timely to grab the price difference. There is no need for an iceberg order. This parameter setting is the same as the number of orders placed.
For example, if the moving average of the price difference is 100, the current price difference is 200, the number of orders placed is 2, and the grid opening price difference is 30, then the positions held at this time are: 6 short positions in the second quarter, 6 permanent short positions, and 12 long positions in the current quarter. If you are not sure, you can look at the code for details.
### Notes
- Delivery contracts require one-way positions, that is, long and short positions are not held at the same time.
- The margin is full position mode.
- This strategy is not a brainless strategy. Test it carefully after understanding the principles.
- The backtest of the research article will not be based on the actual situation, so there is no need to over-optimize the parameters.
- If the robot does not run for a long time, in order to prevent the price difference from being too large, a new robot needs to be created.
- The grid opening price difference parameter must cover the handling fee. For example, the taker handling fee is 20,000 and the Bitcoin price is 10,000. It must be at least greater than 8\*10000\*0.0002=16. Plus a certain margin, it can be set to 25-30.
- As the delivery approaches, the time difference between the second quarter and the current quarter and the current quarter and the perpetuation becomes larger and larger. Finally, the current quarter is close to the perpetuity. Butterfly arbitrage is actually an arbitrage between the second quarter and the perpetuity. It cannot operate and needs to be stopped 2 weeks before delivery or to observe whether it continues to operate. In the same way, new contracts should also be observed.
- When placing an order using IOC, the tradable part will be immediately executed at the entrusted price (or better price), and the part that cannot be fully executed immediately will be cancelled. So there is no need to cancel the order.
- With slight modifications, this strategy can also be changed to arbitrage between the current quarter and perpetual or the second quarter and perpetual.
- The strategy does not open and close positions frequently, and may not open an order in a day.
- The robot will only start to calculate the average price difference when it starts running, and will not trace back the history.
- The strategy is likely to be single-legged due to the failure to close the transaction, and can be optimized by itself.
- The sliding price is added to the order, which has little impact on the number of small open positions. For large open positions, you need to optimize it yourself, such as iceberg orders.










> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Symbol|BTC|Transaction currency|
|Trade_value|true|Number of orders placed|
|Grid|false|Grid opening price difference|
|Alpha|1e-06|Difference smoothing parameter Alpha|
|Ice_value|5|Number of iceberg commissions|

> Source (javascript)

``` javascript
if(IsVirtual()){
    throw '不能回测，回测参考研究文章 https://www.fmz.com/digest-topic/6102'
}
if(exchange.GetName() != 'Futures_Binance'){
    throw '只支持币安期货交易所，和现货交易所不同，需要单独添加，名称为Futures_Binance'
}
if(Grid == 0){
    throw '需要设置网格差价，需要覆盖8份手续费，可设置为当前价*fee*15'
}

exchange.SetBase("https://dapi.binance.com") //切换至交割合约

var exchange_info = HttpQuery('https://dapi.binance.com/dapi/v1/exchangeInfo')
if(!exchange_info){
    throw '无法连接币安网络，需要非公用海外托管者'
}
exchange_info = JSON.parse(exchange_info)
trade_info = {} //合约基础信息
trade_contract = {NEXT_QUARTER:'',CURRENT_QUARTER:'',PERPETUAL:''} //需要交易的合约代码
for (var i=0; i<exchange_info.symbols.length; i++){
   trade_info[exchange_info.symbols[i].symbol] =  exchange_info.symbols[i]
   if(exchange_info.symbols[i].baseAsset == Symbol && exchange_info.symbols[i].contractType in trade_contract && exchange_info.symbols[i].contractStatus == 'TRADING'){
       trade_contract[exchange_info.symbols[i].contractType] = exchange_info.symbols[i].symbol
   }
}
if(!(trade_contract.NEXT_QUARTER && trade_contract.CURRENT_QUARTER && trade_contract.PERPETUAL)){
    throw '无法找到蝶式对冲的三个合约'
}
var pricePrecision = trade_info[trade_contract.PERPETUAL].pricePrecision //价格精度

var ticker = {}
var account = {}
var position = {}

var diff_mean = null //差价均价
if(_G('diff_mean') && _G('symbol') == Symbol){ //防止切换币种，差价出错
    diff_mean = _G('diff_mean')
}else{
    _G('symbol',Symbol)
}

var diff_buy = 0 //做多的差价
var diff_sell = 0 //做空的差价
Trade_value = _N(Trade_value, 0)
 
var init_asset = 0 //初始资金
if(_G('init_asset')){
    init_asset = _G('init_asset')
}else{
    updateAccount()
    init_asset = parseFloat(account[Symbol].marginBalance)
    _G('init_asset', init_asset)
}
var update_status_time = 0
var update_account_time = Date.now()

function onexit(){
    _G('diff_mean', diff_mean)
}

function updateTicker(){
    var bookTicker =  HttpQuery('https://dapi.binance.com/dapi/v1/ticker/bookTicker')
    try {
        bookTicker = JSON.parse(bookTicker)
        for(var i=0;i<bookTicker.length;i++){
            ticker[bookTicker[i].symbol] = bookTicker[i]
        }
    } catch (e) {
        Log('无法获取行情')
    }
}

function updateAccount(){
    var acc = exchange.IO("api", "GET", "/dapi/v1/account", "timestamp="+Date.now())
    if(!acc){
        Log('无法获取账户')
        return
    }
    for(var i=0;i<acc.assets.length;i++){
        account[acc.assets[i].asset] = acc.assets[i]
    }
}

function updatePosition(){
    var pos = exchange.IO("api", "GET", "/dapi/v1/positionRisk", "timestamp="+Date.now())
    if(!pos){
        Log('无法获取仓位')
        return
    }
    for(var i=0;i<pos.length;i++){
        position[pos[i].symbol] = pos[i]
    }
}

function updateStatus(){
    if(Date.now() - update_status_time < 4000){
        return
    }
    update_status_time = Date.now()
    if(Date.now() - update_account_time >  5*60*1000){
        update_account_time = Date.now()
        updateAccount()
        LogProfit(_N(parseFloat(account[Symbol].marginBalance) - init_asset, 5))
    }
    
    $.PlotLine('buy', _N(diff_buy, pricePrecision))
    $.PlotLine('sell', _N(diff_sell, pricePrecision))
    $.PlotLine('mean', _N(diff_mean, pricePrecision+3))
    
    var table1 = {type: 'table', title: '账户信息', 
             cols: ['账户余额', '未实现盈亏', '保证金余额',  '可用余额', '维持保证金', '起始保证金', 'BNB', '初始余额', '收益', '平均差价', '做多差价', '做空差价', '下单量'],
             rows: [[_N(parseFloat(account[Symbol].walletBalance),5), _N(parseFloat(account[Symbol].unrealizedProfit),5), _N(parseFloat(account[Symbol].marginBalance),5), 
                     _N(parseFloat(account[Symbol].availableBalance),5),  _N(parseFloat(account[Symbol].maintMargin),5), _N(parseFloat(account[Symbol].initialMargin),5), 
                     _N(parseFloat(account.BNB.walletBalance),5), _N(init_asset,5),
                      _N(parseFloat(account[Symbol].marginBalance) - init_asset,5), _N(diff_mean, pricePrecision+1),
                     _N(diff_buy, pricePrecision),_N(diff_sell, pricePrecision), Trade_value
                    ]]}
    var table2 = {type: 'table', title: '对冲信息', 
             cols: ['合约', '持仓张数', 'Bid', 'Ask', '持仓价值', '杠杆', '开仓均价', '未实现盈亏'],
             rows: []}
    for(var contract in trade_contract){
        var symbol = trade_contract[contract]
        table2.rows.push([symbol, position[symbol].positionAmt, ticker[symbol].bidPrice, ticker[symbol].askPrice, 
                          parseInt(position[symbol].positionAmt)*parseInt(trade_info[symbol].contractSize), position[symbol].leverage,
                         position[symbol].entryPrice, position[symbol].unRealizedProfit])
    }
    var logString = _D()+'  策略代码最后更新时间9月29日\n'
    LogStatus(logString + '`' + JSON.stringify(table1) + '`'+'\n'+'`' + JSON.stringify(table2) + '`')
}

function trade(symbol, side, price, amount){
    //IOC下单，未成交部分会自动撤销
    exchange.Log(side == 'BUY' ? LOG_TYPE_BUY : LOG_TYPE_SELL, price, amount, ' buy: ' + _N(diff_buy, pricePrecision) + ' sell: '+ _N(diff_sell, pricePrecision) + ' mean: '+_N(diff_mean, pricePrecision+3))
    exchange.IO("api", "POST","/dapi/v1/order","symbol="+symbol+"&side="+side+"&type=LIMIT&timeInForce=IOC&quantity="+amount+"&price="+price+"&timestamp="+Date.now())
}


function onTicker(){
    
    //由于是吃单，需要分别计算做多和做空的差价
    diff_sell = parseFloat(ticker[trade_contract.NEXT_QUARTER].bidPrice) + parseFloat(ticker[trade_contract.PERPETUAL].bidPrice) -
                2*parseFloat(ticker[trade_contract.CURRENT_QUARTER].askPrice)
    diff_buy = parseFloat(ticker[trade_contract.NEXT_QUARTER].askPrice) + parseFloat(ticker[trade_contract.PERPETUAL].askPrice)  -
                2*parseFloat(ticker[trade_contract.CURRENT_QUARTER].bidPrice)

    
    if(!diff_mean){diff_mean = (diff_buy+diff_sell)/2}
    diff_mean = diff_mean*(1-Alpha) + Alpha*(diff_buy+diff_sell)/2 //差价均价的更新
    
    
    var aim_buy_amount = -Trade_value*(diff_buy - diff_mean)/Grid
    var aim_sell_amount = -Trade_value*(diff_sell - diff_mean)/Grid 
    
    if(aim_buy_amount - parseFloat(position[trade_contract.PERPETUAL].positionAmt) > Trade_value){ //做多差价，价格加了滑价
        trade(trade_contract.PERPETUAL, 'BUY', _N(parseFloat(ticker[trade_contract.PERPETUAL].askPrice)*1.01, pricePrecision), _N(Math.min(aim_buy_amount-parseFloat(position[trade_contract.PERPETUAL].positionAmt),Ice_value),0))
    }
    if(aim_buy_amount - parseFloat(position[trade_contract.NEXT_QUARTER].positionAmt) > Trade_value){
        trade(trade_contract.NEXT_QUARTER, 'BUY', _N(parseFloat(ticker[trade_contract.NEXT_QUARTER].askPrice)*1.01,pricePrecision), _N(Math.min(aim_buy_amount-parseFloat(position[trade_contract.NEXT_QUARTER].positionAmt),Ice_value),0))
    }
    if(-2*aim_buy_amount - parseFloat(position[trade_contract.CURRENT_QUARTER].positionAmt) < -2*Trade_value){
        trade(trade_contract.CURRENT_QUARTER, 'SELL', _N(parseFloat(ticker[trade_contract.CURRENT_QUARTER].bidPrice)*0.99,pricePrecision), _N(2*Math.min(aim_buy_amount+parseFloat(position[trade_contract.CURRENT_QUARTER].positionAmt),Ice_value),0))
    }
    
    if(aim_sell_amount - parseFloat(position[trade_contract.PERPETUAL].positionAmt) < -Trade_value){ //做空差价
        trade(trade_contract.PERPETUAL, 'SELL', _N(parseFloat(ticker[trade_contract.PERPETUAL].bidPrice)*0.99,pricePrecision), _N(Math.min(parseFloat(position[trade_contract.PERPETUAL].positionAmt)-aim_sell_amount,Ice_value),0))
    }
    if(aim_sell_amount - parseFloat(position[trade_contract.NEXT_QUARTER].positionAmt) < -Trade_value){
        trade(trade_contract.NEXT_QUARTER, 'SELL', _N(parseFloat(ticker[trade_contract.NEXT_QUARTER].bidPrice)*0.99,pricePrecision), _N(Math.min(parseFloat(position[trade_contract.NEXT_QUARTER].positionAmt)-aim_sell_amount,Ice_value),0))
    }
    if(-2*aim_sell_amount - parseFloat(position[trade_contract.CURRENT_QUARTER].positionAmt) > 2*Trade_value){
        trade(trade_contract.CURRENT_QUARTER, 'BUY', _N(parseFloat(ticker[trade_contract.CURRENT_QUARTER].askPrice)*1.01,pricePrecision), _N(-2*Math.min(aim_sell_amount-parseFloat(position[trade_contract.CURRENT_QUARTER].positionAmt),Ice_value),0))
    }
}

function main() {
    updateAccount()
    updatePosition()
    while(true){
        updateTicker()
        updatePosition()
        onTicker()
        updateStatus()
        Sleep(1*1000)
    }
}
```

> Detail

https://www.fmz.com/strategy/226882

> Last Modified

2021-09-07 14:40:17
