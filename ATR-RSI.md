
> Name

ATR-RSI Combination Strategy
> Author

One knife
> Strategy Description

## Atr indicator
Average True Range (Average True Range), referred to as ATR indicator. It is mainly used to measure the intensity of market fluctuations and show the market change rate, but it cannot reflect the price direction and trend stability. The higher the value of this indicator, the greater the possibility of a trend change, and conversely, the smaller the possibility of a trend change.
### Calculation method
The average true fluctuation range is calculated based on the real fluctuations of the past N days and the real fluctuations of the current day. The true single-day fluctuation is based on the maximum value among the three sets of results: (highest price of the day - lowest price of the day), (highest price of the day - yesterday's closing price), (yesterday's closing price - lowest price of the day), with the purpose of obtaining the price difference within the maximum fluctuation range.
## Rsi indicator
Relative Strength Index (RSI). Technical indicators that determine future market trends by comparing the strength of buying and selling power between long and short parties within a period of time.
### Calculation method
RSI = 100 - (100/(1+RS));
RS = n-day closing number of gains and n-day closing number of decreases;
Generally, RSI uses 50 as the middle line. If it is greater than 50, it is considered a long market, and if it is less than 50, it is considered a short market.
An RSI greater than 70 is considered an overbought state, and the subsequent market may see a correction or a turnaround. An RSI less than 30 is considered an oversold state, and a subsequent rise may occur.
## Strategy Principle
ATR is used for filtering. When ATR>ATRMa (the average ATR of the past N days), it means that the market volatility has begun to increase and the trend is strengthening. RSI is used to generate trading signals.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|rsi_period|20|Strength and weakness indicator calculation period|
|atr_period|14|Average true amplitude calculation period|
|atrma_period|20|Average true volatility and average price calculation period|
|tick_interval|60|Time interval|
|slide_price|0.3|Order sliding value|

> Source (javascript)

``` javascript
/*backtest
start: 2021-02-11 00:00:00
end: 2022-02-10 23:59:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Huobi","currency":"BCH_USDT"}]
args: [["rsi_period",12],["atrma_period",18]]
*/

/*
* rsi_period: 强弱指标计算周期
* atr_period: 平均真实波幅计算周期
* atrma_period: 平均真实波幅均值计算呢周期
* tick_interval: 时间间隔
* slide_price: 下单滑动值
*/

// RSI指示操作状态
var RSI_NONE = 0;
var RSI_BUY = 1;
var RSI_SELL = 2;

var last_rsi_staus;

// ATR活跃信号判断
function isAtrActive(records) {
    let atr = TA.ATR(records, atr_period);
    let atrma = atr[atr.length - 1];
    if (atr.length > atrma_period) {
        let tmp_atr = 0;
        for (let i = atr.length - atrma_period; i < atr.length; i++) {
            tmp_atr += atr[i];
        }
        atrma = tmp_atr / atr_period;
    }
    else {
        atrma = aval(atr.join("+")) / atr.length;
    }
    return atr[atr.length - 1] > atrma;
}

// 获取RSI操作状态
function getRsiStatus(records) {
    let rsi = TA.RSI(records, rsi_period)[records.length - 1];
    if (rsi < 30) {
        return RSI_BUY;
    }
    else if (rsi > 70) {
        return RSI_SELL;
    }
    else {
        return RSI_NONE;
    }
}

// 取消未成交下单
function canelPendingOrders() {
    while (true) {
        let orders = _C(exchange.GetOrders);
        if (orders.length == 0) {
            break;
        }
        for (let i = 0; i < orders.length; i++) {
            exchange.CancelOrder(orders[i].Id);
        }
    }
}

function onTick() {
    let records = _C(exchange.GetRecords, PERIOD_M15);
    let ticker = _C(exchange.GetTicker);
    if (records == null ||
        ticker == null ||
        records.length < rsi_period ||
        records.length < atr_period) {
        return;
    }

    if (isAtrActive(records)) {
        let rsi = getRsiStatus(records);
        if (rsi != RSI_NONE) {
            let account = _C(exchange.GetAccount);
            if (rsi == RSI_BUY && last_rsi_staus != RSI_BUY) {
                Log("买入信号");
                last_rsi_staus = RSI_BUY;
                canelPendingOrders();
                if(account.Balance>0){
                    let price = ticker.Last + slide_price;
                    let amount = account.Balance / price * 0.99;
                    exchange.Buy(price, amount);
                }
            } else if (rsi == RSI_SELL && last_rsi_staus != RSI_SELL) {
                Log("卖出信号");
                last_rsi_staus = RSI_SELL;
                canelPendingOrders();
                if (account.Stocks > 0) {
                    let price = ticker.Last - slide_price;
                    exchange.Sell(price, account.Stocks);
                }
            }
        }
    }
    last_records = records;
}

function main() {
    while (true) {
        onTick();
        Sleep(tick_interval * 1000);
    }
}
```

> Detail

https://www.fmz.com/strategy/345036

> Last Modified

2022-02-13 17:19:57
