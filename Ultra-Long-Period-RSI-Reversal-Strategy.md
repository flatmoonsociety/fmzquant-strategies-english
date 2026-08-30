
> Name

Ultra-Long-Period-RSI-Reversal-Strategy

> Author

ChaoZhang

> Strategy Description


[trans]
Ultra-long period RSI reversal strategy
This strategy calculates the ultra-long period RSI indicator and forms a trading signal based on its intersection with the threshold.
Specifically, it uses a very long period RSI parameter, with typical settings of 50-100 periods. When the RSI indicator goes above the oversold zone, a buy signal is generated; when the RSI indicator goes below the overbought zone, a sell signal is generated.
The advantage of this strategy is that ultra-long period RSI can more accurately judge market trends, filter out short-term market noise, and avoid being trapped. However, the RSI indicator itself has hysteresis and cannot detect trend reversal in time. In addition, parameter settings need to be optimized for different varieties.
In general, the ultra-long period RSI reversal strategy is suitable for medium and long-term positions. Although it performs well, traders still need to pay attention to the risk of trend conversion and stop losses in a timely manner to protect funds. Only by achieving comprehensive risk management can we obtain stable returns in the long term.
||

This strategy uses an ultra long period RSI indicator to generate trading signals based on RSI crossover with thresholds. 

Specifically, it adopts a very long RSI period, typically 50-100. Long signals are triggered when RSI crosses above oversold level. Short signals are generated on RSI crossing below overbought level.

The advantage of this strategy is the ultra long RSI can more precisely determine trend, filtering out short-term noise and avoiding whipsaws. However, RSI itself has lagging issues and cannot promptly detect reversals. Also, parameter tuning is required for different products.

In summary, the ultra long RSI reversal strategy suits medium-long term holding. Despite decent performance, attention is still required on trend change risks and timely stop loss to protect capital. Only with comprehensive risk management can steady profits be achieved in the long run.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|65|length|
|v_input_2|40|overSold|
|v_input_3|60|overBought|
|v_input_4_close|0|price: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-03 00:00:00
end: 2023-09-10 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
// strategy("Kozlod - RSI Strategy - 1 minute", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)


// Inputs
length     = input(65)
overSold   = input(40)
overBought = input(60)
price      = input(close)

// RSI
vrsi = rsi(price, length)

if (crossover(vrsi, overSold))
    strategy.entry("RsiLE", strategy.long, comment="RsiLE")
if (crossunder(vrsi, overBought))
    strategy.entry("RsiSE", strategy.short, comment="RsiSE")

```

> Detail

https://www.fmz.com/strategy/426391

> Last Modified

2023-09-11 17:36:19
