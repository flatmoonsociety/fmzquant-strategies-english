
> Name

Quantitative-Trading-Strategy-Based-on-RSI-Indicator-Signals
> Author

ChaoZhang

> Strategy Description


[trans]

This article will introduce in detail a quantitative strategy that uses the RSI indicator to form trading signals. This strategy processes the RSI indicator and sets the entry and exit conditions for long and short transactions.
1. Strategy Principle
The main trading logic of this strategy is as follows:
1. Calculate the RSI(14) indicator and smooth it using EMA(28) to obtain the processed oscillator indicator.
2. Calculate the Bollinger Bands on the processed RSI indicator to obtain the upper and lower rails. Set overbought and oversold ranges.
3. When the processed RSI indicator crosses the entry line downwards, a buy signal is generated; when it crosses the entry line above, a sell signal is generated.
4. When the indicator enters the overbought and oversold range, a closing signal is generated.
In this way, the characteristics of the RSI indicator can be used to capture reversal opportunities. And perform indicator processing to improve signal quality and reference value.
2. Strategic advantages
The biggest advantage of this strategy is that the indicator processing process increases the parameter space, which can strictly control the trading frequency and avoid over-trading.
Another advantage is that the entry conditions are simple and intuitive, and the trading timing can be judged through the clear value of the indicator.
Finally, the setting of overbought and oversold ranges also helps to stop profits and losses in a timely manner and control the risk of a single transaction.
3. Potential risks
But this strategy also has the following risks:
First of all, the RSI indicator focuses on reversal trading and can easily produce false signals in trends.
Secondly, improper parameter settings can also lead to over-optimization and the inability to adapt to changes in market structure.
Finally, a low winning rate requires a certain amount of loss pressure.
4. Content summary
This article mainly introduces a quantitative trading strategy using the RSI indicator. It controls the trading frequency through parameter adjustment and operates with clear entry and exit rules. While optimizing parameters, it is also necessary to prevent and control the risk of reversal trading. Overall, it provides a simple and intuitive RSI strategy model.
||

This article explains in detail a quantitative trading strategy that utilizes RSI indicator to generate trading signals. It processes the RSI indicator and sets entry and exit criteria for long and short trades.

I. Strategy Logic

The main trading logic is as follows:

1. Compute the RSI(14) indicator and smooth it using EMA(28) to obtain the processed oscillator. 

2. Calculate Bollinger Bands on the processed RSI to get upper/lower bands. Set overbought/oversold zones.

3. When the processed RSI crosses below the entry line, a buy signal is generated. When it crosses above, a sell signal is generated.

4. When the indicator enters the overbought/oversold zones, a close position signal is generated.

In this way, the characteristics of RSI can be utilized to capture reversal opportunities. The indicator processing also improves the signal quality and reference value.

II. Advantages of the Strategy

The biggest advantage is the increased parameter tuning space from indicator processing, which allows tighter control over trade frequency and prevents overtrading.

Another advantage is the intuitive entry criteria based on clear numeric values of the indicator. 

Lastly, the overbought/oversold range also helps with timely profit taking and risk control per trade.

III. Potential Weaknesses

However, the strategy also has the following risks:

Firstly, RSI focuses on reversal trades, which can generate false signals during trends.

Secondly, improper parameter tuning can also lead to over-optimization and failure to adapt to changing market conditions.

Lastly, the relatively low win rate also exposes the strategy to drawdown risks. 

IV. Summary

In summary, this article mainly introduces a quantitative trading strategy utilizing the RSI indicator. It controls trade frequency via parameter tuning and has clear entry/exit rules. While optimizing parameters, risks of reversal trading also need to be managed. Overall, it provides a simple and intuitive RSI strategy framework.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|(?=== RSI ===)RSI|
|v_input_2|28|EMA|
|v_input_3|80|(?=== %b ===)Length|
|v_input_4|3|Multiplier|
|v_input_5|0.8|Overbought|
|v_input_6|0.2|Oversold|
|v_input_7|0.8|Entry Short|
|v_input_8|0.2|Entry Long|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
//-----------------------------------------------------------------
//This simple strategy base on RSI, EMA, Bollinger Bands to get Buy and Sell Signal with detail as below:
//-----------------------------------------------------------------
//1.Define Oscillator Line
//+ Oscillator Line is smoothed by ema(28) of RSI(14) on H1 Timeframe
//2.Define Overbought and Oversold
//+ Apply Bollinger Bands BB(80,3) on Oscillator Line and calculate %b
//+ Overbought Zone marked above level 0.8
//+ Oversold Zone marked below level 0.2
//3.Buy Signal
//+ Entry Long Positon when %b crossover Point of Entry Long
//+ Deafault Point of Entry Long is 0.2
//+ Buy signal marked by Green dot
//4.Sell Signal
//+ Entry Short Position when %b crossunder Point of Entry Short
//+ Deafault Point of Entry Short is 0.8
//+ Sell signal marked by Red dot
//5.Exit Signal
//+ Exit Position (both Long and Short) when %b go into Overbought Zone or Oversold Zone
//+ Exit signal marked by Yellow dot
//-----------------------------------------------------------------
strategy(title="RSI %b Signal [H1 Backtesting]", overlay=false)

//RSI
rsi_gr="=== RSI ==="
rsi_len = input(14, title = "RSI",inline="set",group=rsi_gr)
smoothed_len = input(28, title = "EMA",inline="set",group=rsi_gr)
rsi=ta.ema(ta.rsi(close,rsi_len),smoothed_len)
//rsi's BOLLINGER BANDS
pb_gr="=== %b ==="
length = input(80, title = "Length",inline="set1",group=pb_gr)
rsimult = input(3.0, title = "Multiplier",inline="set1",group=pb_gr)
ovb = input(0.8, title = "Overbought",inline="set2",group=pb_gr)
ovs = input(0.2, title = "Oversold",inline="set2",group=pb_gr)
et_short = input(0.8, title = "Entry Short",inline="set3",group=pb_gr)
et_long = input(0.2, title = "Entry Long",inline="set3",group=pb_gr)
[rsibasis, rsiupper, rsilower] = ta.bb(rsi, length, rsimult)
//rsi's %B
rsipB = ((rsi - rsilower) / (rsiupper - rsilower))
plot(rsipB, title="rsi's %B", color=rsipB>math.min(ovb,et_short)?color.red:rsipB<math.max(ovs,et_long)?color.green:color.aqua, linewidth=1)

h1=hline(1,color=color.new(color.red,100))
h4=hline(ovb,color=color.new(color.red,100))
h0=hline(0,color=color.new(color.green,100))
h3=hline(ovs,color=color.new(color.green,100))
h5=hline(0.5,color=color.new(color.silver,0),linestyle=hline.style_dotted)

fill(h1,h4, title="Resistance", color=color.new(color.red,90))
fill(h0,h3, title="Support", color=color.new(color.green,90))

//Signal
rsi_buy=
           rsipB[1]<et_long
           and
           rsipB>et_long
rsi_sell=
           rsipB[1]>et_short
           and
           rsipB<et_short
rsi_exit=
           (rsipB[1]>ovs and rsipB<ovs)
           or
           (rsipB[1]<ovb and rsipB>ovb)
plotshape(rsi_buy?rsipB:na,title="Buy",style=shape.circle,color=color.new(color.green,0),location=location.absolute)
plotshape(rsi_sell?rsipB:na,title="Sell",style=shape.circle,color=color.new(color.red,0),location=location.absolute)
plotshape(rsi_exit?rsipB:na,title="Exit",style=shape.circle,color=color.new(color.yellow,0),location=location.absolute)
//Alert
strategy.entry("Long",strategy.long,when=rsi_buy)
strategy.close("Long",when=rsi_exit)
strategy.entry("Short",strategy.short,when=rsi_sell)
strategy.close("Short",when=rsi_exit)
//EOF
```

> Detail

https://www.fmz.com/strategy/426852

> Last Modified

2023-09-14 20:26:49
