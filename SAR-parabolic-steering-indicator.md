
> Name

SAR parabolic steering indicator
> Author

Taofen Quantification
> Strategy Description

This strategy is modified based on "One Moving Average Trend Demo" by Diandouzi (https://www.fmz.com/strategy/193609），
Using the signal of the Parabolic SAR as a buying and selling point is a digital currency futures trend strategy.
The drawing code uses Zero's "Line Drawing Class Library" (https://www.fmz.com/strategy/27293），
Refer to Xiaoxiaomeng's "Example of Drawing K-Line and Moving Average Charts Using Line Drawing Library" (https://www.fmz.com/strategy/125770）。
———— Taofen Quantification (WeChat: himandy)


=====I am the low-key dividing line======
A good trading platform can make your strategy skyrocket. If you register through the link, you can get a VIP5 handling fee discount for two months:
(Spot: 0% for pending orders, 0.07% for takers. Contract: 0% for pending orders, 0.04% for takers)
https://www.kucoin.center/ucenter/signup?rcode=1wxJ2fQ&lang=zh_CN&utmsource=VIP_TF
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Amount|100|Amount|
|time_interval|3600|Customized K-line period (seconds)|

> Source (javascript)

``` javascript
/*backtest
start: 2017-11-01 00:00:00
end: 2020-09-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_BitMEX","currency":"XBT_USD"}]
args: [["Amount",10000],["time_interval",86400]]
*/

/*
本策略基于扁豆子的《一根均线 趋势 Demo》（https://www.fmz.com/strategy/193609）进行修改，使用抛物线转向指标SAR的信号作为买卖点，属于数字货币期货趋势策略。

画图代码使用了Zero的《画线类库》（https://www.fmz.com/strategy/27293），参考了小小梦的《使用画线类库画K线以及均线图表范例》（https://www.fmz.com/strategy/125770）。

———— 韬奋量化（微信：himandy）
*/

// 定义对象

//用于回测
if (IsVirtual) {
    if (exchange.GetCurrency() == "BTC_USD") {
        exchange.SetContractType("quarter"); //选择合约
    } else if (exchange.GetCurrency() == "XBT_USD") {
        exchange.SetContractType("XBTUSD"); //便于策略选择BitMEX回测
    }
}

exchange.SetMarginLevel(1)

var LastBarTime = 0,
    Idle = -1,
    status = Idle;

var preAccount, account, records, ticker, balance, Bar;
var sar, isFirst, PreBarTime, preTime;

// 链接交易所, 获取相关信息
function UpdateInfo() {
    account = exchange.GetAccount()
    records = exchange.GetRecords(time_interval)
    ticker = exchange.GetTicker()
    //balance = account.Stocks
    //Bar = records[records.length - 1]
}

// 指标计算获取
function Get_SAR() {
    sar = talib.SAR(records, 0.02, 0.2);
}

// 开平仓规则
function onTick() {

    ticker = exchange.GetTicker()
    if (status === Idle) {
        if (ticker.Last > sar[sar.length - 1]) {
            exchange.SetDirection("buy")
            exchange.Buy(ticker.Sell, Amount)
            status = PD_LONG
            $.PlotFlag(new Date().getTime(), 'Buy', 'BK');
        } else if (ticker.Last < sar[sar.length - 1]) {
            exchange.SetDirection("sell")
            exchange.Sell(ticker.Buy, Amount)
            status = PD_SHORT
            $.PlotFlag(new Date().getTime(), 'Sell', 'SK');
        }
    } else if (status === PD_LONG) {
        if (ticker.Last < sar[sar.length - 1]) {
            exchange.SetDirection("closebuy")
            exchange.Sell(ticker.Buy, Amount)
            account = exchange.GetAccount()
            status = Idle
            $.PlotFlag(new Date().getTime(), 'CloseBuy', 'SP');
        }
    } else if (status === PD_SHORT) {
        if (ticker.Last > sar[sar.length - 1]) {
            exchange.SetDirection("closesell")
            exchange.Buy(ticker.Sell, Amount)
            account = exchange.GetAccount()
            status = Idle
            $.PlotFlag(new Date().getTime(), 'CloseSell', 'BP');
        }
    }

}

function PlotMA_Kline(records, isFirst) {

    $.PlotRecords(records, "BTC")
    if (isFirst) {
        for (var i = records.length - 1; i >= 0; i--) {
            if (sar[i] !== null) {
                $.PlotLine("SAR", sar[i], records[i].Time);
            }
        }
        PreBarTime = records[records.length - 1].Time;
    } else {
        if (PreBarTime !== records[records.length - 1].Time) {
            $.PlotLine('SAR', sar[sar.length - 2], records[records.length - 2].Time);
            PreBarTime = records[records.length - 1].Time;
        }
        $.PlotLine('SAR', sar[sar.length - 1], records[records.length - 1].Time);
    }
}

function main() {
    preAccount = exchange.GetAccount()
    // 链接交易所, 获取相关信息
    UpdateInfo()

    // 主函数, 不停循环
    while (1) {
        records = exchange.GetRecords(time_interval)
        preTime = records[records.length - 1].Time
        //机器人延时等待，直至下一个K线周期，单位是毫秒
        while (new Date().getTime() < (preTime + time_interval * 1000)) { //把K线周期转换为毫秒
            records = exchange.GetRecords(time_interval)
            // 指标计算获取
            Get_SAR()
            // 开平仓规则
            onTick()
            // 轮询sleep时间
            Sleep(5 * 1000)
        }

        //画线
        if (records) {
            PlotMA_Kline(records, isFirst);
            isFirst = false;
        }

        // 打印balance
        LogProfit(account.Stocks - preAccount.Stocks, "&")

    }
}
```

> Detail

https://www.fmz.com/strategy/224799

> Last Modified

2021-11-02 10:53:24
