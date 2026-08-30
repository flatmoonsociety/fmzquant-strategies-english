
> Name

Over-sold, over-rising, super bullish version
> Author

ChaoZhang

> Strategy Description

## 4.13 Updates
Stop_loss is set to 0.8, which means that when the funds reach less than 80% of the initial funds, the loss will be stopped, all positions will be cleared, and the strategy will be stopped. As the strategy runs, Stop_loss can be set greater than 1 (restart to take effect). For example, if you earn 1,500 from 1,000, and Stop_loss is set to 1.3, then the stop loss will be retraced to 1,300 yuan. If you don't want to stop the loss, you can set this parameter very small. The risk is that if everyone uses this kind of stop loss, it will cause a stampede and increase losses. The initial funds are in the init_balance field of the status bar. Please note that operations such as withdrawals will be affected. Don't accidentally stop the loss. If you are still afraid of black swan events, such as a certain currency returning to 0, you can withdraw it manually.
Max_diff and Min_diff limit the degree of deviation and need to be determined by yourself based on your own trade_value, total funds and risk tolerance.
To give a simple example, if a total of 20 coins are traded, and the value of one coin gradually rises to deviate from 0.4 and is no longer traded, the prices of other coins will remain unchanged, resulting in a loss of 7 times the trade_value. If it continues to fall to a deviation of -0.3, it will lose 6 times of trade_value.
```
var Stop_loss = 0.8 
var Max_diff = 0.4 //当偏差diff大于0.4时，不继续加空仓, 自行设置
var Min_diff = -0.3 //当diff小于-0.3时，不继续加多仓, 自行设置
```

## 4.10 Updates
**Copy the strategy code to the local strategy, overwrite and save it directly, restart the robot to take effect, and the original position will be maintained**
Important optimization notebook code address for Binance Futures short over-rising, long over-sold strategy: https://www.fmz.com/bbs-topic/5364
Original strategy altcoin index = mean(sum((altcoin price/bitcoin price)/(altcoin initial price/bitcoin initial price))). The biggest problem is that the comparison between the latest price and the initial price when the strategy is started will deviate more and more as time goes by. A coin may hold many positions, which is very risky. In the end, it will hold many positions, increasing risks and drawdowns.
The latest altcoin index = mean(sum((altcoin price/bitcoin price)/EMA(altcoin price/bitcoin price))), which is compared with the price of the moving average, can track the latest price changes, is more flexible, and backtesting has found that it reduces strategic positions and also reduces retracements. More stable. The most important thing is that if a few abnormal trading pairs are added to the original strategy, the risk is extremely high and the position is likely to be liquidated, but now it is almost unaffected.
For a seamless upgrade, two of the parameters are written into the first two lines of the policy code and can be changed as needed.
Alpha = 0.04 The Alpha parameter of the exponential moving draw, the larger the setting, the more sensitive the benchmark price tracking will be, the fewer transactions will be made, and the final position will be lower, which reduces the leverage, but will reduce the income, reduce the maximum retracement, and increase the trading volume. You need to weigh it based on the backtest results.
Update_base_price_time_interval = 30*60 How often to update the base price, in seconds, related to the Alpha parameter. The smaller the Alpha is set, the smaller the interval can be set.
If you read the article and want to trade all currencies, here is the list ``ETH, BCH, XRP, EOS, LTC, TRX, ETC, LINK, XLM, ADA,
## **Important content! ! **
- Be sure to read this study https://www.fmz.com/digest-topic/5294 first. Understand the strategy principles, risks, how to screen trading pairs, how to set parameters, the ratio of opening positions to total funds, and a series of other issues.
- The previous research report needs to be downloaded and uploaded to your own research environment. Run the actual modifications. If you've seen this report, it was recently updated with data for the latest week.
- **The strategy cannot be backtested directly and needs to be backtested in a research environment**.
- The strategy code and default parameters are for research only. You need to be cautious when running real trading. Decide parameters based on your own research. **At your own risk**.
- **The strategy cannot be profitable every day. You can look at the backtest history. Sideways and retracements in 1-2 weeks are normal and need to be treated correctly**
- The code is public and can be modified by yourself. If you have any questions, please leave comments and feedback. It is best to join the inventor Binance exchange group (how to join is in the research report) to get update notifications.
- **The strategy only supports Binance futures and needs to be run in cross position mode. Do not set two-way positions! ! , just use the default trading pair and K-line cycle when creating the robot. The strategy does not use K-line**
- **Strategies conflict with other strategies and manual operations and need to be noted**
- Real-time operation requires an overseas host. During the test phase, you can rent an Alibaba Cloud Hong Kong server with one click on the platform. It is cheaper to rent the entire server by yourself on a monthly basis (the lowest configuration is enough, deployment tutorial: https://www.fmz.com/bbs-topic/2848)
- Binance’s futures and spot need to be added separately. Binance futures is ``Futures_Binance``
- Restarting this strategy will not affect it, but creating a new robot will re-record historical data.
- The strategy may be updated based on user feedback. Just ctrl+A to copy the code and save it (generally the parameters will not be updated). Restart the robot to use the latest code.
- The strategy does not allow trading at the beginning. Data needs to be recorded when starting for the first time, and you need to wait for market changes before trading.
## Join the WeChat group to participate in the Binance Thousand Group War to get updates
Add the WeChat ID below and reply "Binance" to automatically join the group:
https://www.fmz.com![IMG](assets/images/08fb0f6e5844d67fc05e61bd37543a321dc60c1e6b2bf4ba1b9064ed195b2049.jpg)

## Strategy Principle
We will short the currency whose price is higher than the altcoin-Bitcoin price index and long the currency whose price is lower than the index. The greater the deviation, the larger the position. (This strategy does not use BTC to hedge unequal positions. BTC can also be added to the trading pair). Performance in the past two months (about 3 times leverage, data updated to 4.8):
 ![IMG](assets/images/28f4cf764481b87db49d93e23aa3904cc95cebd65cac2d350e1e177ea09776c1.png)
## Strategy logic
1. Update market conditions and account positions. The initial price will be recorded during the first run (newly added currencies are calculated based on the time of addition)
2. Update the index. The index is Altcoin-Bitcoin price index = mean(sum((Altcoin price/Bitcoin price)/(Altcoin initial price/Bitcoin initial price)))
3. Determine long and short positions based on the deviation index, and determine positions based on the size of the deviation.
4. Place an order. The order quantity is determined by Bingshan Commission, and the transaction is completed according to the opponent's price (buy at the same price as the sell). **Cancel the order immediately after placing it (so you will see many orders with failed cancellation 400: {"code":-2011,"msg":"Unknown order sent."}, which is normal)**
5. Cycle again
The level in the status bar represents the proportion of margin used, which needs to be kept low to meet new openings.
## Strategy parameters
 ![IMG](assets/images/1db2260b20ab52334af839b288bb2c34a0c7247d73c804e5944ab58b5526b8eb.png) 

- Trade_symbols: The currency for trading, you need to filter it yourself according to the research platform, you can also add BTC
- Trade_value: Every time the altcoin price (priced in BTC) deviates from the index by 1%, the holding value needs to be determined based on the total funds invested and risk preference. It is recommended to set it to 3-10% of the total funds. The size of the leverage can be seen through backtesting in the research environment. Trade_value can be less than Adjust_value, such as half of Adjust_value, which is equivalent to a holding value that deviates from the index by 2%.
- Adjust_value: The contract value (priced in USDT) adjusts the deviation value. When the index deviates from \* Trade_value - current position > Adjust_value, that is, the difference between the target position and the current position exceeds this value, a transaction will start. If it is too large, the adjustment will be slow. If it is too small, transactions will be frequent. It cannot be lower than 10, otherwise the minimum transaction will not be reached. It is recommended to set it to more than 40% of Trade_value.
- Ice_value: The iceberg commission value cannot be less than 10. When placing an order, choose the smaller one between Adjust_value and Ice_value. If you have more funds, you can set it relatively larger so that the adjustment can be faster. It is recommended not to be lower than 20% of Adjust_value, so that the transaction can be completed after 5 times of iceberg. Of course, when the Trade_value is not large, Ice_value can be set relatively large, and the adjustment can be completed in one or two times.
- Interval: The cycle sleep time can be set smaller, such as 1s, but it cannot exceed the Binance frequency limit.
- Reset: Reset historical data, which will reset the initial price of the strategy reference to the current price. Generally, there is no need to set it.

## Strategy Risk
Note that if a certain currency goes out of independent market, for example, it rises several times compared to the index, a large number of short positions will be accumulated on the currency. The same sharp decline will also cause the strategy to go long in large quantities. You can limit the opening amount or stop loss and no longer trade.


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Trade_symbols|IOST,TRX,XLM,QTUM,DASH,ADA,BNB,XMR,ZEC,ATOM,IOTA,NEO,ONT,XRP,BAT,VET,EOS,ETC,LTC|Trading currencies|
|Trade_value|20|Holding value for every 1% deviation from the index|
|Adjust_value|20|Contract value adjustment deviation value|
|Ice_value|20|Size of iceberg order|
|Log_profit_interval|600|Log total equity interval s|
|Interval|true|sleep time s|
|Reset|false|Reset historical data|

> Source (javascript)

``` javascript

/*
 * @Description: 加分号版,首先这是一个山寨版,添加的功能已经在下面,没有动过逻辑上的内容
 * @Version: 0.1.3
 * @Author: RedSword
 * @Email: redsword@gamil.com
 * @Date: 2020-04-10 11:48:38
 * @LastEditors: Home RedSword
 * @LastEditTime: 2020-04-18 19:49:28
 *
 * 运行之前,一定要仔细的看草神的文章,地址 https://www.fmz.com/strategy/195226
 * 
 * 添加功能
 * 
 * 2020-04-18
 * 1.添加草神的均衡对冲功能
 * 2.修改了默认Alpha值和基准价格更新时间,Alpha改为了0.001,基准价格更新时间改为了1分钟
 * 3.添加强平距离以及百分比
 * 4.修改偏离平均和各币种的预估胜率放到了币指数信息里
 * 5.屏蔽了Log收益的功能,省点空间
 * 
 * 2020-04-16
 * 1.修复了月亮走我也走的BUG
 * 2.修复了添加新币种出错的BUG
 * 
 * 2020-04-15
 * 1.添加账户资产信息
 * 2.添加币种指数信息
 * 3.添加各币种的胜率
 * 4.添加单币种投降功能
 * 5.感谢fmzero开源的代码
 * 
 * 2020-04-13
 * 1.添加交易相关的统计,感谢豆子开源的代码
 * 2.带预估字样的,都是不准的,只能做大概的参考
 * 3.加入草神最新的止损逻辑
 * 4.删除原有Max_amount的止损方法
 * 5.添加显示绝对收益的开关
 * 6.显示原版策略的提示,在盈利统计加了止损的提示
 * 
 * 2020-04-12
 * 1.添加了最大开仓量限制,0为不限制
 * 2.持仓价值显示绝对值,不显负号
 * 3.显示当前币种杠杆倍数和持仓强平价格
 * 4.添加币种的开仓模式,全仓或者逐仓
 * 5.修正重置不起作用的BUG
 * 6.修改运行时间不准的BUG
 * 7.修改保证金显示,和官方一至
 * 8.保证金不显示比例,改为比率,和官方一至
 * 
 * 2020-04-10
 * 1.给强迫症加了分号
 * 2.添加了盈利统计
 * 3.添加了开仓方向,并对持仓方向和持仓盈亏做了颜色区分
 */

var Alpha = 0.001; //指数移动平均的Alpha参数，设置的越大，基准价格跟踪越敏感，最终持仓也会越低，降低了杠杆，但会降低收益，具体需要根据回测结果自己权衡
var Update_base_price_time_interval = 60; //多久更新一次基准价格, 单位秒，和Alpha参数相关,Alpha 设置的越小，这个间隔也可以设置的更小



//Stop_loss设置为0.8表示当资金达到低于初始资金的80%时，止损，清空所有仓位，停止策略。
//随着策略运行，Stop_loss可以设置大于1（重启生效），比如从1000赚到1500，Stop_loss设置为1.3，则回撤到1300元止损。不想止损可以把这个参数设置的很小。
//风险是大家都用这种止损会形成踩踏，加大亏损。
//初始资金在状态栏的init_balance字段，注意提现等操作会影响，别不小心止损了。
//如果还是怕黑天鹅事件，比如某个币归0等，可以手动提现出来。

var Stop_loss = 0.8;
var Max_diff = 0.4; //当偏差diff大于0.4时，不继续加空仓, 自行设置
var Min_diff = -0.3; //当diff小于-0.3时，不继续加多仓, 自行设置

var Version = '0.1.3';
var Show = false; //默认为false累计收益显示是账户余额,改为true累计收益显示为收益,如果之前是显示的账户余额,你使用LogProfitReset()来清空图表
var Funding = 0; //账户初始金额,为0的时候,自动获取,非0为自定义
var Success = '#5cb85c'; //成功颜色
var Danger = '#ff0000'; //危险颜色
var Warning = '#f0ad4e'; //警告颜色
var RunTime; //运行时间
var SelfFee = '0.04'; //https://www.binance.com/cn/fee/futureFee
var TotalLong;
var TotalShort;
var UpProfit = 0;
var accountAssets = []; //保存资产
var WinRateData = {}; //保存所有币种的胜率及开仓次数

if (IsVirtual()) {
    throw '不能回测，回测参考 https://www.fmz.com/digest-topic/5294 ';
}
if (exchange.GetName() != 'Futures_Binance') {
    throw '只支持币安期货交易所，和现货交易所不同，需要单独添加，名称为Futures_Binance';
}
var trade_symbols = Trade_symbols.split(',');
var symbols = trade_symbols;
var index = 1; //指数
if (trade_symbols.indexOf('BTC') < 0) {
    symbols = trade_symbols.concat(['BTC']);
}
var update_profit_time = 0;
var update_base_price_time = Date.now();
var assets = {};
var init_prices = {};
var trade_info = {};

function init() {
    InitRateData();
    var exchange_info = HttpQuery('https://fapi.binance.com/fapi/v1/exchangeInfo');
    if (!exchange_info) {
        throw '无法连接币安网络，需要海外托管者';
    }
    exchange_info = JSON.parse(exchange_info);
    for (var i = 0; i < exchange_info.symbols.length; i++) {
        if (symbols.indexOf(exchange_info.symbols[i].baseAsset) > -1) {
            assets[exchange_info.symbols[i].baseAsset] = {
                amount: 0,
                hold_price: 0,
                value: 0,
                bid_price: 0,
                ask_price: 0,
                btc_price: 0,
                btc_change: 1,
                btc_diff: 0,
                realised_profit: 0,
                margin: 0,
                unrealised_profit: 0,
                leverage: 20,
                positionInitialMargin: 0,
                liquidationPrice: 0
            };
            trade_info[exchange_info.symbols[i].baseAsset] = {
                minQty: parseFloat(exchange_info.symbols[i].filters[1].minQty),
                priceSize: parseInt((Math.log10(1.1 / parseFloat(exchange_info.symbols[i].filters[0].tickSize)))),
                amountSize: parseInt((Math.log10(1.1 / parseFloat(exchange_info.symbols[i].filters[1].stepSize))))
            };
        }
    }
}
assets.USDT = {
    unrealised_profit: 0,
    margin: 0,
    margin_balance: 0,
    total_balance: 0,
    leverage: 0,
    update_time: 0,
    margin_ratio: 0,
    init_balance: 0,
    stop_balance: 0,
    short_value: 0,
    long_value: 0,
    profit: 0
};

function updateAccount() { //更新账户和持仓
    var account = exchange.GetAccount();
    var pos = exchange.GetPosition();
    if (account == null || pos == null) {
        Log('update account time out');
        return;
    }
    accountAssets = account.Info.assets;
    assets.USDT.update_time = Date.now();
    for (var i = 0; i < trade_symbols.length; i++) {
        assets[trade_symbols[i]].margin = 0;
        assets[trade_symbols[i]].unrealised_profit = 0;
        assets[trade_symbols[i]].hold_price = 0;
        assets[trade_symbols[i]].amount = 0;
    }
    for (var j = 0; j < account.Info.positions.length; j++) {
        if (account.Info.positions[j].positionSide == 'BOTH') {
            var pair = account.Info.positions[j].symbol;
            var coin = pair.slice(0, pair.length - 4);
            if (trade_symbols.indexOf(coin) < 0) {
                continue;
            }
            assets[coin].margin = parseFloat(account.Info.positions[j].initialMargin) + parseFloat(account.Info.positions[j].maintMargin);
            assets[coin].unrealised_profit = parseFloat(account.Info.positions[j].unrealizedProfit);
            assets[coin].positionInitialMargin = parseFloat(account.Info.positions[j].positionInitialMargin);
            assets[coin].leverage = account.Info.positions[j].leverage;
        }
    }
    assets.USDT.margin = _N(parseFloat(account.Info.totalInitialMargin) + parseFloat(account.Info.totalMaintMargin), 2);
    assets.USDT.margin_balance = _N(parseFloat(account.Info.totalMarginBalance), 2);
    assets.USDT.total_balance = _N(parseFloat(account.Info.totalWalletBalance), 2);
    if (assets.USDT.init_balance == 0) {
        if (_G('init_balance')) {
            assets.USDT.init_balance = _N(_G('init_balance'), 2);
        } else {
            assets.USDT.init_balance = assets.USDT.total_balance;
            _G('init_balance', assets.USDT.init_balance);
        }
    }
    assets.USDT.profit = _N(assets.USDT.margin_balance - assets.USDT.init_balance, 2);
    assets.USDT.stop_balance = _N(Stop_loss * assets.USDT.init_balance, 2);
    assets.USDT.total_balance = _N(parseFloat(account.Info.totalWalletBalance), 2);
    assets.USDT.unrealised_profit = _N(parseFloat(account.Info.totalUnrealizedProfit), 2);
    assets.USDT.leverage = _N(assets.USDT.margin / assets.USDT.total_balance, 2);
    assets.USDT.margin_ratio = (account.Info.totalMaintMargin / account.Info.totalMarginBalance * 100);
    pos = JSON.parse(exchange.GetRawJSON());
    if (pos.length > 0) {
        for (var k = 0; k < pos.length; k++) {
            var pair = pos[k].symbol;
            var coin = pair.slice(0, pair.length - 4);
            if (trade_symbols.indexOf(coin) < 0) {
                continue;
            }
            if (pos[k].positionSide != 'BOTH') {
                continue;
            }
            assets[coin].hold_price = parseFloat(pos[k].entryPrice);
            assets[coin].amount = parseFloat(pos[k].positionAmt);
            assets[coin].unrealised_profit = parseFloat(pos[k].unRealizedProfit);
            assets[coin].liquidationPrice = parseFloat(pos[k].liquidationPrice);
            assets[coin].marginType = pos[k].marginType;
        }
    }
}

function updateIndex() { //更新指数
    if (!_G('init_prices') || Reset) {
        Reset = false;
        for (var i = 0; i < trade_symbols.length; i++) {
            init_prices[trade_symbols[i]] = (assets[trade_symbols[i]].ask_price + assets[trade_symbols[i]].bid_price) / (assets.BTC.ask_price + assets.BTC.bid_price);
        }
        Log('保存启动时的价格');
        _G('init_prices', init_prices);
        _G("StartTime", null); //重置开始时间
        _G("initialAccount_" + exchange.GetLabel(), null); //重置开始资金
        _G("tradeNumber", null); //重置交易次数
        _G("tradeVolume", null); //重置交易量
        _G("buyNumber", null); //重置做多次数
        _G("sellNumber", null); //重置做空次数
        _G("totalProfit", null); //重置打印次数
        _G("profitNumber", null); //重置盈利次数
    } else {
        init_prices = _G('init_prices');
        if (Date.now() - update_base_price_time > Update_base_price_time_interval * 1000) {
            update_base_price_time = Date.now();
            for (var i = 0; i < trade_symbols.length; i++) { //更新初始价格
                init_prices[trade_symbols[i]] = init_prices[trade_symbols[i]] * (1 - Alpha) + Alpha * (assets[trade_symbols[i]].ask_price + assets[trade_symbols[i]].bid_price) / (assets.BTC.ask_price + assets.BTC.bid_price);
            }
            _G('init_prices', init_prices);
        }
        var temp = 0;
        for (var i = 0; i < trade_symbols.length; i++) {
            assets[trade_symbols[i]].btc_price = (assets[trade_symbols[i]].ask_price + assets[trade_symbols[i]].bid_price) / (assets.BTC.ask_price + assets.BTC.bid_price);
            if (!(trade_symbols[i] in init_prices)) {
                Log('添加新的币种', trade_symbols[i]);
                init_prices[trade_symbols[i]] = assets[trade_symbols[i]].btc_price;
                _G('init_prices', init_prices);
            }
            assets[trade_symbols[i]].btc_change = _N(assets[trade_symbols[i]].btc_price / init_prices[trade_symbols[i]], 4);
            temp += assets[trade_symbols[i]].btc_change;
        }
        index = _N(temp / trade_symbols.length, 4);
    }

}

function updateTick() { //更新行情
    var ticker = HttpQuery('https://fapi.binance.com/fapi/v1/ticker/bookTicker');
    try {
        ticker = JSON.parse(ticker);
    } catch (e) {
        Log('get ticker time out');
        return;
    }
    assets.USDT.short_value = 0;
    assets.USDT.long_value = 0;
    for (var i = 0; i < ticker.length; i++) {
        var pair = ticker[i].symbol;
        var coin = pair.slice(0, pair.length - 4);
        if (symbols.indexOf(coin) < 0) {
            continue;
        }
        assets[coin].ask_price = parseFloat(ticker[i].askPrice);
        assets[coin].bid_price = parseFloat(ticker[i].bidPrice);
        assets[coin].ask_value = _N(assets[coin].amount * assets[coin].ask_price, 2);
        assets[coin].bid_value = _N(assets[coin].amount * assets[coin].bid_price, 2);
        if (trade_symbols.indexOf(coin) < 0) {
            continue;
        }
        if (assets[coin].amount < 0) {
            assets.USDT.short_value += Math.abs((assets[coin].ask_value + assets[coin].bid_value) / 2);
        } else {
            assets.USDT.long_value += Math.abs((assets[coin].ask_value + assets[coin].bid_value) / 2);
        }
        assets.USDT.short_value = _N(assets.USDT.short_value, 0);
        assets.USDT.long_value = _N(assets.USDT.long_value, 0);
    }
    updateIndex();
    for (var i = 0; i < trade_symbols.length; i++) {
        assets[trade_symbols[i]].btc_diff = _N(assets[trade_symbols[i]].btc_change - index, 4);
    }
}



function trade(symbol, dirction, value) { //交易
    if (Date.now() - assets.USDT.update_time > 10 * 1000) {
        Log('更新账户延时，不交易');
        return;
    }
    var price = dirction == 'sell' ? assets[symbol].bid_price : assets[symbol].ask_price;
    var amount = _N(Math.min(value, Ice_value) / price, trade_info[symbol].amountSize);
    if (amount < trade_info[symbol].minQty) {
        Log(symbol, '合约价值偏离或冰山委托订单的大小设置过小，达不到最小成交, 至少需要: ', _N(trade_info[symbol].minQty * price, 0) + 1);
        return;
    }
    exchange.IO("currency", symbol + '_' + 'USDT');
    exchange.SetContractType('swap');
    exchange.SetDirection(dirction);
    var f = dirction == 'buy' ? 'Buy' : 'Sell';
    var id = exchange[f](price, amount, symbol);
    if (id) {
        exchange.CancelOrder(id); //订单会立即撤销
    }
    tradingCounter("tradeVolume", price * amount); //保存交易量
    tradingCounter("tradeNumber", 1); //保存交易次数
    WinRateData[symbol].tradeNumber += 1;
    if (dirction == 'buy') {
        tradingCounter("buyNumber", 1);
        WinRateData[symbol].buyNumber += 1;
    } else {
        tradingCounter("sellNumber", 1);
        WinRateData[symbol].sellNumber += 1;
    }
    _G("WinRateData", WinRateData); //保存各币种的交易数据
    return id;
}

function InitRateData() {
    if (Reset) {
        _G("WinRateData", null);
    }
    if (_G("WinRateData")) {
        WinRateData = _G("WinRateData");
    }
    for (var i = 0; i < symbols.length; i++) {
        if (typeof WinRateData[symbols[i]] == 'undefined') {
            WinRateData[symbols[i]] = {
                totalProfit: 0, //统计次数
                profitNumber: 0, //盈利次数
                tradeNumber: 0, //交易次数
                buyNumber: 0, //做多次数
                sellNumber: 0 //做空次数
            };
        }
    }
    _G("WinRateData", WinRateData);
}

function RunCommand() {
    var str_cmd = GetCommand();
    if (str_cmd) {
        var arrCmd = str_cmd.split(':');
        var symbol = arrCmd[1];
        var amount = parseFloat(arrCmd[2]);
        if (amount == 0) {
            Log('亲,你还记得大明湖畔的乔碧萝吗?' + Danger);
            return;
        }
        var f = amount < 0 ? 'Buy' : 'Sell';
        var dirction = amount < 0 ? 'buy' : 'sell';
        exchange.IO("currency", symbol + '_' + 'USDT');
        exchange.SetContractType('swap');
        exchange.SetDirection(dirction);
        exchange[f](-1, Math.abs(amount), symbol);
    }
}

function FirstAccount() {
    var key = "initialAccount_" + exchange.GetLabel();
    var initialAccount = _G(key);
    if (initialAccount == null) {
        initialAccount = exchange.GetAccount();
        _G(key, initialAccount);
    }
    return initialAccount;
}

function StartTime() {
    var StartTime = _G("StartTime");
    if (StartTime == null) {
        StartTime = _D();
        _G("StartTime", StartTime);
    }
    return StartTime;
}

function RuningTime() {
    var ret = {};
    var dateBegin = new Date(StartTime());
    var dateEnd = new Date(_D());
    var dateDiff = dateEnd.getTime() - dateBegin.getTime();
    var dayDiff = Math.floor(dateDiff / (24 * 3600 * 1000));
    var leave1 = dateDiff % (24 * 3600 * 1000);
    var hours = Math.floor(leave1 / (3600 * 1000));
    var leave2 = leave1 % (3600 * 1000);
    var minutes = Math.floor(leave2 / (60 * 1000));
    ret.dayDiff = dayDiff;
    ret.hours = hours;
    ret.minutes = minutes;
    ret.str = "运行时间: " + dayDiff + " 天 " + hours + " 小时 " + minutes + " 分钟";
    return ret;
}

function AppendedStatus() {
    var accountTable = {
        type: "table",
        title: "盈利统计",
        cols: ["运行天数", "初始资金", "现有资金", "保证金余额", "已用保证金", "保证金比率", "止损", "总收益", "预计年化", "预计月化", "平均日化"],
        rows: []
    };
    var feeTable = {
        type: 'table',
        title: '交易统计',
        cols: ["策略指数", '交易次数', '做多次数', '做空次数', '预估胜率', '预估成交额', '预估手续费', "未实现盈利", '持仓总值', '做多总值', '做空总值'],
        rows: []
    };
    var runday = RunTime.dayDiff;
    if (runday == 0) {
        runday = 1;
    }
    if (Funding == 0) {
        Funding = parseFloat(FirstAccount().Info.totalWalletBalance);
    }
    var profitColors = Danger;
    var totalProfit = assets.USDT.total_balance - Funding; //总盈利
    if (totalProfit > 0) {
        profitColors = Success;
    }
    var dayProfit = totalProfit / runday; //天盈利
    var dayRate = dayProfit / Funding * 100;
    accountTable.rows.push([
        runday,
        '$' + _N(Funding, 2),
        '$' + assets.USDT.total_balance,
        '$' + assets.USDT.margin_balance,
        '$' + assets.USDT.margin,
        _N(assets.USDT.margin_ratio, 2) + '%',
        _N(assets.USDT.stop_balance, 2) + Danger,
        _N(totalProfit / Funding * 100, 2) + "% = $" + _N(totalProfit, 2) + (profitColors),
        _N(dayRate * 365, 2) + "% = $" + _N(dayProfit * 365, 2) + (profitColors),
        _N(dayRate * 30, 2) + "% = $" + _N(dayProfit * 30, 2) + (profitColors),
        _N(dayRate, 2) + "% = $" + _N(dayProfit, 2) + (profitColors)
    ]);
    var vloume = _G("tradeVolume") ? _G("tradeVolume") : 0;
    feeTable.rows.push([
        index, //指数
        _G("tradeNumber") ? _G("tradeNumber") : 0, //交易次数
        _G("buyNumber") ? _G("buyNumber") : 0, //做多次数
        _G("sellNumber") ? _G("sellNumber") : 0, //做空次数
        _N(_G("profitNumber") / _G("totalProfit") * 100, 2) + '%', //胜率
        '$' + _N(vloume, 2) + ' ≈ ฿' + _N(vloume / ((assets.BTC.bid_price + assets.BTC.ask_price) / 2), 6), //成交金额
        '$' + _N(vloume * (SelfFee / 100), 4), //手续费
        '$' + _N(assets.USDT.unrealised_profit, 2) + (assets.USDT.unrealised_profit >= 0 ? Success : Danger),
        '$' + _N(TotalLong + Math.abs(TotalShort), 2), //持仓总价值
        '$' + _N(TotalLong, 2) + Success, //做多总值
        '$' + _N(Math.abs(TotalShort), 2) + Danger, //做空总值
    ]);
    var assetTable = {
        type: 'table',
        title: '账户资产信息',
        cols: ['编号', '资产名', '起始保证金', '维持保证金', '保证金余额', '最大可提款金额', '挂单起始保证金', '持仓起始保证金', '持仓未实现盈亏', '账户余额'],
        rows: []
    };
    for (var i = 0; i < accountAssets.length; i++) {
        var acc = accountAssets[i];
        assetTable.rows.push([
            i + 1,
            acc.asset, acc.initialMargin, acc.maintMargin, acc.marginBalance,
            acc.maxWithdrawAmount, acc.openOrderInitialMargin, acc.positionInitialMargin,
            acc.unrealizedProfit, acc.walletBalance
        ]);
    }
    var indexTable = {
        type: 'table',
        title: '币指数信息',
        cols: ['编号', '币种信息', '当前价格', 'BTC计价', 'BTC计价变化(%)', '偏离平均', '交易次数', '做空次数', '做多次数', '预估胜率'],
        rows: []
    };
    for (var i = 0; i < symbols.length; i++) {
        var price = _N((assets[symbols[i]].ask_price + assets[symbols[i]].bid_price) / 2, trade_info[symbols[i]].priceSize);
        if (symbols.indexOf(symbols[i]) < 0) {
            indexTable.rows.push([i + 1, symbols[i], price, assets[symbols[i]].btc_price, _N((1 - assets[symbols[i]].btc_change) * 100), assets[symbols[i]].btc_diff], 0, 0, 0, '0%');
        } else {
            var rateData = _G("WinRateData");
            var winRate = _N(rateData[symbols[i]].profitNumber / rateData[symbols[i]].totalProfit * 100, 2);
            indexTable.rows.push([
                (i + 1),
                symbols[i] + Warning,
                price,
                _N(assets[symbols[i]].btc_price, 6),
                _N((1 - assets[symbols[i]].btc_change) * 100),
                assets[symbols[i]].btc_diff + (assets[symbols[i]].btc_diff >= 0 ? Success : Danger),
                rateData[symbols[i]].tradeNumber,
                rateData[symbols[i]].sellNumber,
                rateData[symbols[i]].buyNumber,
                (rateData[symbols[i]].profitNumber > 0 && rateData[symbols[i]].totalProfit > 0 ? winRate : '0') + '%' + (winRate >= 50 ? Success : Danger), //胜率
            ]);
        }
    }
    var retData = {};
    retData.upTable = RunTime.str + '\n' + "最后更新: " + _D() + '\n' + 'Version:' + Version + '\n' + '`' + JSON.stringify([accountTable, assetTable]) + '`\n' + '`' + JSON.stringify(feeTable) + '`\n';
    retData.indexTable = indexTable;
    return retData;
}

function WinRate() {
    for (var i = 0; i < symbols.length; i++) {
        var unrealised = assets[symbols[i]].unrealised_profit;
        WinRateData[symbols[i]].totalProfit += 1;
        if (unrealised != 0) {
            if (unrealised > 0) {
                WinRateData[symbols[i]].profitNumber += 1;
            }
        }
    }
    _G("WinRateData", WinRateData);
}


function tradingCounter(key, newValue) {
    var value = _G(key);
    if (!value) {
        _G(key, newValue);
    } else {
        _G(key, value + newValue);
    }
}

function updateStatus() { //状态栏信息
    var table = {
        type: 'table',
        title: '交易对信息',
        cols: ['编号', '[模式][倍数]', '币种信息', '开仓方向', '开仓数量', '持仓价格', '当前价格', '强平价格', '强平差价', '持仓价值', '保证金', '未实现盈亏', '投降'],
        rows: []
    };
    TotalLong = 0;
    TotalShort = 0;
    for (var i = 0; i < symbols.length; i++) {
        var direction = '空仓';
        var margin = direction;
        if (assets[symbols[i]].amount != 0) {
            direction = assets[symbols[i]].amount > 0 ? '做多' + Success : '做空' + Danger;
            margin = (assets[symbols[i]].marginType == 'cross' ? '全仓' : '逐仓');
        }

        var price = _N((assets[symbols[i]].ask_price + assets[symbols[i]].bid_price) / 2, trade_info[symbols[i]].priceSize);
        var value = _N((assets[symbols[i]].ask_value + assets[symbols[i]].bid_value) / 2, 2);
        if (value != 0) {
            if (value > 0) {
                TotalLong += value;
            } else {
                TotalShort += value;
            }
        }
        // var rateData = _G("WinRateData");
        var infoList = [
            i + 1,
            "[" + margin + "] [" + assets[symbols[i]].leverage + 'x] ',
            symbols[i],
            direction,
            Math.abs(assets[symbols[i]].amount),
            assets[symbols[i]].hold_price,
            price,
            assets[symbols[i]].liquidationPrice, //强平价格
            assets[symbols[i]].liquidationPrice == 0 ? '0' : '$' + _N(assets[symbols[i]].liquidationPrice - price, 5) + ' ≈ ' + _N(assets[symbols[i]].liquidationPrice / price * 100, 2) + '%' + Warning, //强平价格
            Math.abs(value),
            _N(assets[symbols[i]].positionInitialMargin, 2),
            // assets[symbols[i]].btc_diff,
            _N(assets[symbols[i]].unrealised_profit, 3) + (assets[symbols[i]].unrealised_profit >= 0 ? Success : Danger),
            // (rateData[symbols[i]].profitNumber > 0 && rateData[symbols[i]].totalProfit > 0 ? _N(rateData[symbols[i]].profitNumber / rateData[symbols[i]].totalProfit * 100, 2) : '0') + '%', //胜率
            {
                'type': 'button',
                'cmd': '说好的没有撤退可言呢？？?:' + symbols[i] + ':' + assets[symbols[i]].amount + ':',
                'name': symbols[i] + ' 投降'
            }
        ];
        table.rows.push(infoList);
    }
    delete assets.USDT.update_time; //时间戳没什么用,不要了
    var logString = JSON.stringify(assets.USDT) + '\n';
    var StatusData = AppendedStatus();
    LogStatus(StatusData.upTable + '`' + JSON.stringify([table, StatusData.indexTable]) + '`\n' + logString);

    if (Date.now() - update_profit_time > Log_profit_interval * 1000) {
        var balance = assets.USDT.margin_balance;
        if (Show) {
            balance = assets.USDT.margin_balance - Funding;
        }
        LogProfit(_N(balance, 3), '&');
        update_profit_time = Date.now();
        if (UpProfit != 0 && (_N(balance, 0) != UpProfit)) { //第一次不计算,并且小数点面的不进行胜率计算
            tradingCounter("totalProfit", 1); //统计打印次数, 胜率=盈利次数/打印次数*100
            if (_N(balance, 0) > UpProfit) {
                tradingCounter("profitNumber", 1); //盈利次数
            }
            WinRate();
        }
        UpProfit = _N(balance, 0);
    }

}

function stopLoss() { //止损函数
    while (true) {
        if (assets.USDT.margin_balance < Stop_loss * assets.USDT.init_balance && assets.USDT.init_balance > 0) {
            Log('触发止损，当前资金：', assets.USDT.margin_balance, '初始资金：', assets.USDT.init_balance);
            Ice_value = 200; //止损的快一些，可修改
            updateAccount();
            updateTick();
            var trading = false; //是否正在交易
            for (var i = 0; i < trade_symbols.length; i++) {
                var symbol = trade_symbols[i];
                if (assets[symbol].ask_price == 0) {
                    continue;
                }
                if (assets[symbol].bid_value >= trade_info[symbol].minQty * assets[symbol].bid_price) {
                    trade(symbol, 'sell', assets[symbol].bid_value);
                    trading = true;
                }
                if (assets[symbol].ask_value <= -trade_info[symbol].minQty * assets[symbol].ask_price) {
                    trade(symbol, 'buy', -assets[symbol].ask_value);
                    trading = true;
                }
            }
            Sleep(1000);
            if (!trading) {
                throw '止损结束,如果需要重新运行策略，需要调低止损';
            }
        } else { //不用止损
            return;
        }
    }
}

function onTick() { //策略逻辑部分
    for (var i = 0; i < trade_symbols.length; i++) {
        var symbol = trade_symbols[i];
        if (assets[symbol].ask_price == 0) {
            continue;
        }
        var aim_value = -Trade_value * _N(assets[symbol].btc_diff / 0.01, 3);
        if (aim_value - assets[symbol].ask_value >= Adjust_value && assets[symbol].btc_diff > Min_diff && assets.USDT.long_value - assets.USDT.short_value <= 1.1 * Trade_value) {
            trade(symbol, 'buy', aim_value - assets[symbol].ask_value);
        }
        if (aim_value - assets[symbol].bid_value <= -Adjust_value && assets[symbol].btc_diff < Max_diff && assets.USDT.short_value - assets.USDT.long_value <= 1.1 * Trade_value) {
            trade(symbol, 'sell', -(aim_value - assets[symbol].bid_value));
        }
    }
}

function main() {
    SetErrorFilter("502:|503:|tcp|character|unexpected|network|timeout|WSARecv|Connect|GetAddr|no such|reset|http|received|EOF|reused|Unknown");
    while (true) {
        RunTime = RuningTime();
        RunCommand(); //捕获交互命令
        updateAccount(); //更新账户和持仓
        updateTick(); //行情
        stopLoss(); //止损
        onTick(); //策略逻辑部分
        updateStatus(); //输出状态栏信息
        Sleep(Interval * 1000);
    }
}
```

> Detail

https://www.fmz.com/strategy/196784

> Last Modified

2020-05-06 10:45:30
