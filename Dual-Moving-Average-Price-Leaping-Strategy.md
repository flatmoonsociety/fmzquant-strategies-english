
> Name

Dual-Moving-Average-Price-Leaping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/cac824aa4c268f43f9fa18c1bdc4dd6a5eece1f99fe9ec134b07d4a93c97ec40.png)

[trans]

### Overview
This strategy uses the RSI indicator to determine overbought and oversold, and combines the trend judgment system constructed by the fast line, the middle line, and the slow line to judge opportunities to open long and short positions when the price jumps.
### Strategy Principles
1. Use RSI indicator to determine overbought and oversold
- RSI parameters are set to 14 periods
  - The oversold line is 30 and the overbought line is 70
2. Use three SMA moving averages with different periods to determine the trend.
- The fast line is the 9-period SMA, which represents the short-term trend
  - The midline is the 50-period SMA, which represents the mid-term trend
  - The slow line is the 200-period SMA, which represents the long-term trend
3. When the fast line crosses the middle line and the RSI indicator shows oversold, enter the market long.
4. When the fast line crosses the middle line and the RSI indicator shows overbought, enter the market short.
5. Stop loss is set to 4% of the entry price
6. The profit method is to take profit in batches, first take profit by 20%, then when the price continues to rise, take profit by 15%, and exit the position in sequence.
### Advantage Analysis
1. Use three SMA moving averages with different periods to judge trend changes in different time periods.
2. Use the RSI indicator to avoid opening positions in areas that are not overbought or oversold.
3. Taking profits in batches increases the strategic position holding period and also increases the average profit of the position.
### Risk Analysis
1. The probability of three moving averages sending wrong signals
2. Taking profit in batches involves the risk of not all transactions being completed.
3. You need to choose appropriate stock varieties, suitable for stocks with large price fluctuations
### Strategy optimization direction
1. You can test and modify the parameters of moving average and RSI to optimize entry and exit opportunities.
2. You can add other indicators to filter candle shapes, etc. to improve the accuracy of the strategy.
3. You can further control risks through dynamic tracking stop loss
### Summarize
This strategy combines the moving average indicator and the overbought and oversold indicator RSI to capture the price change trend and judge buying and selling opportunities at the same time. It is a relatively common trend-tracking strategy. Through parameter testing and adding other auxiliary judgment indicators, the strategy winning rate can be further optimized and improved.
||

### Overview

This strategy uses the RSI indicator to determine overbought and oversold conditions, combined with a trend judgment system constructed with fast, medium and slow moving average lines, to identify opportunities to open long or short positions when prices are leaping.

### Strategy Principle  

1. Use RSI indicator to determine overbought and oversold conditions

    - RSI parameter is set to 14 periods
    - Oversold line is at 30, overbought line is at 70

2. Use three SMA lines of different periods to determine the trend

    - Fast line is 9-period SMA, representing short-term trend 
    - Medium line is 50-period SMA, representing medium-term trend
    - Slow line is 200-period SMA, representing long-term trend

3. When fast line crosses above medium line, and RSI indicator shows oversold, go long

4. When fast line crosses below medium line, and RSI indicator shows overbought, go short

5. Stop loss is set at 4% of entry price  

6. Profit taking is done in batches, first take profit of 20%, then take 15% as price continues to rise, exiting positions gradually

### Advantage Analysis

1. Using three SMA lines of different periods can judge trend changes across different time frames
2. The use of RSI indicator avoids opening positions outside of overbought/oversold areas
3. Batch profit taking increases holding period and average profit of the strategy

### Risk Analysis  

1. Probability of wrong signals from the three moving average lines
2. Risk of incomplete batch profit taking execution 
3. Need to choose suitable instruments with high price fluctuation

### Optimization Directions  

1. Can test modifying parameters of moving averages and RSI to optimize entry and exit
2. Can add other indicators to filter candle patterns etc to improve accuracy 
3. Can dynamically trail stop loss to further control risk

### Summary  

This strategy combines moving average indicators and the overbought/oversold indicator RSI. By capturing price trend changes while judging trading opportunities, it belongs to a commonly used trend tracking strategy. Further optimizations and improved win rate can be achieved through parameter testing and incorporating additional auxiliary judgment indicators.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|oversold|
|v_input_2|70|overbought|
|v_input_3|20|SellPct|
|v_input_4|15|ExitPct|
|v_input_5|9|v_input_5|
|v_input_6|50|v_input_6|
|v_input_7|200|v_input_7|
|v_input_8|100|v_input_8|
|v_input_9|12|Lookback Long Period|
|v_input_10|2|Lookback Short Period|
|v_input_11|4|v_input_11|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-13 00:00:00
end: 2023-11-20 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © syfuslokust

//@version=4
strategy(shorttitle='CoinruleCombinedCryptoStrat',title='CoinruleCombinedCryptoStrat', overlay=true)


// RSI inputs and calculations
lengthRSI = 14
RSI = rsi(close, lengthRSI)
//Normal
oversold = input(30)
overbought =  input(70)
//ALGO
//oversold= input(26)
//overbought= input(80)

//sell pct
SellPct = input(20)
ExitPct = input(15)

//MA inputs and calculations
movingaverage_signal = sma(close, input(9))
movingaverage_fast = sma(close, input(50))
movingaverage_slow = sma(close, input(200))
movingaverage_mid= sma(close, input(100))

//Look Back
inp_lkb = input(12, title='Lookback Long Period')
inp_lkb_2 = input(2, title='Lookback Short Period')
 
perc_change(lkb) =>
    overall_change = ((close[0] - close[lkb]) / close[lkb]) * 100

//Entry 

//MA
bullish = crossover(movingaverage_signal, movingaverage_fast)
//Execute buy
strategy.entry(id="long", long = true, when = (RSI < oversold and movingaverage_fast < movingaverage_mid))

//when = crossover(close, movingaverage_signal) and movingaverage_signal < movingaverage_slow and RSI < oversold)

//Exit

//RSI
Stop_loss= ((input (4))/100)
longStopPrice  = strategy.position_avg_price * (1 - Stop_loss)
//MA
bearish = crossunder(movingaverage_signal, movingaverage_fast)
//Execute sell
strategy.close("long", qty_percent = SellPct, when = RSI > overbought and movingaverage_fast > movingaverage_mid)
//when = (crossunder(low, movingaverage_signal) and movingaverage_fast > movingaverage_slow and RSI > overbought) or (movingaverage_signal < movingaverage_fast and crossunder(low, movingaverage_fast)) or (low < longStopPrice))


//PLOT
plot(movingaverage_signal, color=color.black, linewidth=2, title="signal")
plot(movingaverage_fast, color=color.orange, linewidth=2, title="fast")
plot(movingaverage_slow, color=color.purple, linewidth=2, title="slow")
plot(movingaverage_mid, color=color.blue, linewidth=2, title="mid")
```

> Detail

https://www.fmz.com/strategy/432781

> Last Modified

2023-11-21 14:28:35
