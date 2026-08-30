
> Name

Price-Extreme-Reversion-Strategy-Based-on-Binomial-Distribution
> Author

ChaoZhang

> Strategy Description



[trans]
The name of this strategy is "Price Extreme Value Regression Strategy Based on Binomial Distribution". This strategy uses the binomial distribution function to determine the probability of price reversal, and sets a double EMA moving average strategy to generate trading signals.
The calculation logic of the strategy is as follows:
1. Calculate the number of closing price increases in the last 20 K lines, and count the proportion p of the rising cycle in the past 100 K lines.
2. Bring the number of rising cycles and probability p into the binomial distribution function, and calculate the cumulative distribution function (CDF).
3. Calculate the 10-day and 20-day EMAs for CDF respectively. When the fast line crosses the slow line, it is believed that the probability of the price returning to its extreme value is greater, and a buy signal is generated.
4. When the fast line crosses the slow line, the price may be at a short-term high, and a sell signal is generated.
The advantage of this strategy is that it uses probabilistic methods to determine the timing of extreme price return. However, parameters need to be adjusted according to the market to avoid generating too many false signals.
Generally speaking, statistical methods help to objectively discover price behavior patterns. But in the end, traders still need to maintain keen judgment on the market and properly use technical indicators as auxiliary tools.


||



This strategy is named “Price Extreme Reversion Strategy Based on Binomial Distribution”. It uses the binomial distribution function to estimate the probability of price reversals and sets a dual-EMA system to generate trade signals.

The logic is:

1. Calculate the number of up close bars in the recent 20 bars, and the percentage p of up periods in the past 100 bars.

2. Plug the up period counts and probability p into the binomial distribution function to compute the cumulative distribution function (CDF).

3. Apply 10-day and 20-day EMAs to the CDF. When the fast EMA crosses above the slow EMA, it signals a high probability of price extreme reversion, generating buy signals. 

4. When the fast EMA crosses below the slow EMA, prices may be peaking in the short run, producing sell signals here.

The advantage of this strategy is estimating price extreme reversion timing through probability methods. But parameters need market-adjusted optimization to avoid excessive false signals.

In conclusion, statistical techniques help uncover price behavior patterns objectively. But ultimately, traders still need keen market judgment to use technical indicators as supplementary tools.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-06 00:00:00
end: 2023-05-01 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © pieroliviermarquis

//@version=4
strategy("Binomial Strategy", overlay=false, default_qty_type= strategy.percent_of_equity, default_qty_value= 100, slippage=1, initial_capital= 10000, calc_on_every_tick=true)


factorial(length) =>
    n = 1
    if length != 0
        for i = 1 to length
            n := n * i
    n


binomial_pdf(success, trials, p) =>
    q = 1-p
    coef = factorial(trials) / (factorial(trials-success) * factorial(success))
    pdf = coef * pow(p, success) * pow(q, trials-success)
        
        
binomial_cdf(success, trials, p) =>
    q = 1-p
    cdf = 0.0
    for i = 0 to success
        cdf := cdf + binomial_pdf(i, trials, p)
        

up = close[0] > close[1] ? 1 : 0


//long-term probabilities
lt_lookback = 100
lt_up_bars = sum(up, lt_lookback)
prob = lt_up_bars/lt_lookback


//lookback for cdf
lookback = 20
up_bars = sum(up, lookback)
cdf = binomial_cdf(up_bars, lookback, prob)


//ema on cdf
ema1 = ema(cdf, 10)
ema2 = ema(cdf, 20)


plot(cdf*100)
plot(ema1*100, color=color.red)
plot(ema2*100, color=color.orange)


buy = ema1 > ema2
sell = ema1 < ema2


//////////////////////Bar Colors//////////////////

var color buy_or_sell = na

if buy == true
    buy_or_sell := #3BB3E4
else if sell == true
    buy_or_sell := #FF006E
    
barcolor(buy_or_sell)

///////////////////////////Orders////////////////

if buy
    strategy.entry("Long", strategy.long, comment="")

if sell
    strategy.close("Long", comment="Sell")

```

> Detail

https://www.fmz.com/strategy/426601

> Last Modified

2023-09-13 16:47:22
