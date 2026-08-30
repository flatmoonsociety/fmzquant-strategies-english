
> Name

Scalping-Strategy-Based-on-Market-Liquidity-and-Trend
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c3a9e1d77657d124f2.png)
 [trans]
### Overview
This strategy comprehensively considers multiple dimensions such as market liquidity, trends and technical indicators to achieve short-term strategic trading. This strategy can follow the trend and take advantage of the market liquidity to open positions to obtain short-term profits.
### Strategy Principles
1. Basic principle: This strategy mainly considers the two dimensions of market liquidity and trend. Carry out short-term operations when market liquidity is good and trends emerge.
2. Market liquidity indicator: This strategy mainly uses MFI and trading volume changes as market liquidity indicators. When MFI rises and trading volume rises, we believe that the market liquidity is better and it is suitable to open a position.
3. Trend judgment: This strategy combines ADX, EMA and other indicators to judge the trend. A stronger trend is indicated when ADX is above 30 and its EMA. At the same time, if a golden cross occurs on the fast and slow EMA, the trend can also be verified.
4. Conditions for opening a position: When market liquidity is good and a trend occurs at the same time, if other auxiliary conditions (such as SAR position judgment, etc.) are also met, a position opening signal will be generated.
5. Take profit and stop loss settings: This strategy sets a fixed take profit (10 points) and stop loss (7.5 points) for each transaction.
### Advantage Analysis
This strategy has the following advantages:
1. Use market liquidity to judge timing: Judge market liquidity based on MFI and trading volume to avoid opening positions when market liquidity is poor.
2. Follow the trend to obtain profits: Combine with EMA and other indicators to determine the trend direction and help obtain trend profits.
3. Risk control is in place: fixed stop-profit and stop-loss are set up to effectively control the maximum loss in a single transaction.
4. Higher trading frequency: As a short-term strategy, the trading frequency will be relatively high, which is suitable for gradually accumulating profits.
5. There is a large space for parameter optimization: for example, MA parameters, stop loss and profit settings, etc. can be optimized to improve the strategy effect.

### Risk Analysis
This strategy also has some risks:
1. Real offer slippage control risk: Theoretical stop loss and take profit cannot fully reflect the actual offer situation, and the slippage in the actual offer may be relatively large.
2. Risk of failure in trend judgment: This strategy relies on many indicators for trend judgment, but there is still a possibility of failure.
3. Over-trading risk: As a short-term strategy, improper parameter settings may lead to over-trading.
4. Risk of abnormal market conditions: This strategy may not work properly under extreme circumstances such as extremely poor market liquidity or policy changes.
Correspondingly, we can reduce risks from the following aspects:
1. Appropriately relax the stop loss range and consider the factors of firm slippage.
2. Optimize the trend judgment logic, introduce more indicators, and reduce the probability of failure.
3. Add position opening frequency limit to avoid excessive trading.
4. Flexibly adjust parameters according to market conditions to respond to abnormal situations.
### Optimization direction
The optimization directions of this strategy include:
1. Introduce more indicators to optimize trend judgment and make the judgment more accurate. For example, introduce the MACD indicator, etc.
2. Optimize the period parameters of MA and find the best parameter combination.
3. Improve stop-loss and stop-profit strategies, such as using trailing stop loss, range stop loss, etc.
4. Add limits to the number of transactions to avoid excessively frequent transactions. For example, a maximum of 3 positions can be opened per day.
5. Look for better market liquidity indicators to further determine the timing of opening a position. For example, introduce indicators such as net inflows.
6. Add parameter optimization function to realize automatic parameter optimization and find the optimal parameter combination.
### Summarize
This strategy comprehensively considers multiple dimensions such as market liquidity and trends to capture profits in the short term. Compared with traditional trend strategies, the biggest innovation of this strategy is the introduction of market liquidity indicators to avoid opening positions when market liquidity is poor. Correspondingly, this strategy also has certain risks of firm control and trend judgment failure. We can continue to improve this strategy by introducing more indicators, optimization parameters, and risk management.
||

### Overview  

This strategy comprehensively considers market liquidity, trend and technical indicators to implement short-term trading strategies. The strategy can follow the trend and open positions when market liquidity is relatively good, thereby obtaining short-term profits.

### Strategy Principle  

1. Basic Principle: This strategy mainly considers market liquidity and trend. Carry out short-term operations when market liquidity is good and a trend appears.

2. Market Liquidity Indicators: This strategy mainly uses MFI and changes in trading volume as market liquidity indicators. When MFI goes up and trading volume goes up, we believe that market liquidity is better and it is suitable to open positions.

3. Trend Judgment: This strategy combines ADX, EMA and other indicators to determine the trend. When ADX is above 30 and its EMA, it means that the trend is relatively strong. At the same time, if the golden cross of fast and slow EMA occurs, the trend can also be verified.

4. Opening Conditions: When market liquidity is good and a trend appears at the same time, if other auxiliary conditions (such as SAR position judgment, etc.) are also met, opening signals are generated.

5. Take Profit and Stop Loss Settings: This strategy sets fixed take profit (10 points) and stop loss (7.5 points) for each trade.

### Advantage Analysis   

This strategy has the following advantages:

1. Use market liquidity to determine timing: Based on MFI and trading volume to determine market liquidity, avoid opening positions when market liquidity is poor.

2. Follow trends for profits: Combine EMA and other indicators to determine trend direction, help obtain trend profits.   

3. Good risk control: Set fixed take profit and stop loss to effectively control the maximum loss per trade.

4. Relatively high trading frequency: As a short-term strategy, trading frequency will be relatively high, suitable for accumulating profits step by step.  

5. Large space for parameter optimization: For example, MA parameters, stop loss and take profit settings can be optimized to improve strategy performance.

### Risk Analysis

This strategy also has some risks:   

1. Real trading slippage control risk: Theoretical stop loss and take profit cannot fully reflect real trading conditions. Slippage in real trading may be relatively large.

2. Trend misjudgment risk: This strategy relies heavily on multiple indicators to determine the trend, but there is still a possibility of failure.

3. Over trading risk: As a short-term strategy, improper parameter settings may lead to over trading.  

4. Market anomaly risk: In extreme cases of extremely poor market liquidity or policy changes, this strategy may not work properly.

Correspondingly, we can reduce risks from the following aspects:  

1. Appropriately relax the stop loss range to consider real slippage factors.

2. Optimize trend judgment logic and introduce more indicators to reduce failure probability.   

3. Add open position frequency limits to avoid over trading.  

4. Flexibly adjust parameters based on market conditions to deal with abnormal situations.

### Optimization Direction  

The optimization directions of this strategy include:  

1. Introduce more indicators to optimize trend judgment and make judgments more accurate. For example, introduce MACD indicators, etc.

2. Optimize the cycle parameters of MA to find the best parameter combination. 

3. Improve stop loss and take profit strategies, such as using moving stop loss, interval stop loss and so on.

4. Add restrictions on number of trades to avoid excessively high frequency trading. For example, open positions up to 3 times per day at most.
   
5. Find better market liquidity indicators to further determine timing of opening positions. For example, introduce net inflow indicators.  

6. Add parameter optimization functions to automatically optimize parameters to find optimal parameter combinations.  

### Summary  

This strategy comprehensively considers factors such as market liquidity and trend. It captures profits in the short term. Compared with traditional trend strategies, the biggest innovation of this strategy is the introduction of market liquidity indicators to avoid opening positions when market liquidity is poor. Correspondingly, this strategy also has certain real-world control risks and trend misjudgment risks. We can continuously improve this strategy through introducing more indicators, optimizing parameters, and risk management.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © trent777brown

//@version=5
strategy("scalping with market facilitation", overlay=true, margin_long=100, margin_short=100)


MFI0 = (high - low) / volume
MFI1 = (high[1] - low[1]) / volume[1]

MFIplus = MFI0 > MFI1
MFIminus = MFI0 < MFI1

//Current Trend-(Changed mean to trend)-revised
trendplus = hl2 > high[1]
trendzero = hl2 < high[1] and hl2 > low[1]  //addition of script
trendminus = hl2 < low[1]  //changed high to low

//Volume +/-
volplus = volume > volume[1]
volminus = volume < volume[1]

//Period Control by Buyers or Sellers is determined with reference to Price action of the period 
//divided into 3 sectors, sector 1 is the Top third, Sector 2 is the middle third, 
//and sector 3 is the Bottom third of the period. Control classifications are: Extremes(11, 33), Neutral(22), 
//Climbers(31,21,32) Open lower than Close, and Drifters(13,23,12)Close lower than Open

//value0 = low
//value1 = ((high - low)/3)
//value2 = ((high - low)/3)*2
//value3 = high

//o1 = (open >= (((high - low)/3) * 2) + low)
//c1 = (close >= (((high - low)/3) * 2) + low)
//o2 = (open <= o1) 
//c2 = (close <= c1)
//o3 = (open <= ((high - low)/3) + low)
//c3 = (close <= ((high - low)/3) + low)

//sector2 = if((high - low)/3) + low and sector2 <= (((high - low)/3)*2) + low

//sector3 = if((high - low)/3) + low and >= low


//Extremes-Full Control of Period by Buyers or Sellers 
//pg79 notes an 85% chance that the current trend will change in the next 1 to 5 bars
b11 = open >= (high - low) / 3 * 2 + low and close >= (high - low) / 3 * 2 + low  //Extreme Buyer Control:Chartruse
b33 = open <= (high - low) / 3 + low and close <= (high - low) / 3 + low  //Extreme Seller Control:Crimson
//Neutral pg80
b22 = open >= (high - low) / 3 + low and open <= (high - low) / 3 * 2 and close >= (high - low) / 3 + low and open <= (high - low) / 3 * 2  //Bracketed Price Control
//Climber-Open lower than Close pg81
b31 = open <= (high - low) / 3 + low and close >= (high - low) / 3 * 2 + low  //Strong Buyer Control:Dark Green
b21 = open >= (high - low) / 3 + low and open <= (high - low) / 3 * 2 and close >= (high - low) / 3 * 2 + low  //Moderate Buyer Control:Green
b32 = open <= (high - low) / 3 + low and close >= (high - low) / 3 + low and open <= (high - low) / 3 * 2  //Weak Buyer Control:Light Green
//Drifter-Close lower than Open pg81
b13 = open >= (high - low) / 3 * 2 + low and close <= (high - low) / 3 + low  //Strong Seller Control:Dark Red
b23 = open >= (high - low) / 3 + low and open <= (high - low) / 3 * 2 and close <= (high - low) / 3 + low  //Moderate Seller Control:Red
b12 = open >= (high - low) / 3 * 2 + low and close >= (high - low) / 3 + low and open <= (high - low) / 3 * 2  //Weak Seller Control:Light Red/Pink

 

//


psar= ta.sar(.09, .2, .2)

ema8= ta.ema(hlc3, 8)

ema13h= ta.ema(high, 13)
ema13l= ta.ema(low, 13)
ema13= ta.ema(close, 13)

ema55= ta.ema(close, 100)

[dip, dim, adx]= ta.dmi(5, 5)
adxema=ta.ema(adx, 3)
[macdl, sigl, histl]= ta.macd(close, 8, 13, 5)
obv= ta.obv
obvema= ta.ema(obv, 8)
obvema55= ta.ema(obv, 55)
mfigreen= MFIplus and volplus
adx_x_over= ta.crossover(adx, adxema) and adx >= 25
barssincemfi= ta.barssince(mfigreen)










longtrig2= adx > 30 and adx > adxema and barssincemfi <= 4 


shorttrig2= adx > 30 and adx > adxema and barssincemfi <= 4 


long= macdl > sigl and obv > obvema55 and ema8 > ema55   and psar < low and trendplus//and ema13l > ema55//and open > hull200 and close > hull200

short= macdl < sigl and obv < obvema55 and ema8 < ema55 and psar > high and trendminus//and ema13h < ema55//open < hull200 and close < hull200


//plot(hull200, color=color.red, linewidth=3)
plot(ema13h, color=color.gray, linewidth=3)
plot(ema13l, color=color.gray, linewidth=3)

plot(ema13, color=color.blue, linewidth=3)
//
plot(ema55, color=color.white, linewidth=3)
plot(psar, color=color.white, style=plot.style_circles)
plotshape(mfigreen, color=color.yellow, style=shape.flag, location=location.belowbar, size= size.tiny)
longCondition = long
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long, 1,  when= longtrig2)
    strategy.exit("exit long", "My Long Entry Id", profit= 100, loss= 75)
shortCondition = short
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short, 1,  when= shorttrig2)
    strategy.exit("exit short", "My Short Entry Id", profit= 100, loss= 75)

```

> Detail

https://www.fmz.com/strategy/440435

> Last Modified

2024-01-30 15:36:33
