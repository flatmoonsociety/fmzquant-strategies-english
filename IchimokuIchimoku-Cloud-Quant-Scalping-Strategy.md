
> Name

Ichimoku Cloud Quant Short-term Strategy Ichimoku-Cloud-Quant-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/bc453357c5296e6683a5aa71382d129ff622cdcd9b333340aacd78d35aceb318.png)
[trans]

## Overview
Ichimoku Cloud Quant Scalping Strategy is a short-term quantitative strategy that combines the Ichimoku Balance Sheet and the average direction index. This strategy uses the Ichimoku cloud indicator to determine the trend direction, cooperates with the ADX indicator to filter non-trending markets, and performs short-term operations in trending markets.
## Strategy Principle
This strategy mainly consists of two parts:
1. Ichimoku Cloud Indicator Determines Trend Direction
- Conversion Line: the median line of the last 7 periods
    - Base Line: the median line of the last 26 periods
    - Leading Span A: The midpoint of Conversion Line and Base Line
    - Leading Span B: The median line of the last 52 periods    
When the price is above the cloud, it is a bullish trend, and when the price is below the cloud, it is a bearish trend. The strategy uses the breakthrough of the Conversion Line to judge the turning point of the trend.    
2. ADX indicator filters non-trending markets
When ADX is greater than 20, it indicates a trending market, and then the strategy generates trading signals. When it is less than 20, it means consolidation, and the strategy does not trade at this time.
Trading rules:
- Long entry: price breaks above the Conversion Line and ADX is greater than 20
- Short entry: price breaks below the Conversion Line and ADX is greater than 20
- Stop loss: 150 pips
- Take profit: 200 pips
## Advantage Analysis
This strategy has the following advantages:
1. Riding the trend and avoiding consolidation. The Ichimoku cloud indicator can accurately determine the trend direction and turning point, and cooperate with the ADX indicator to filter and consolidate the market to avoid false breakthroughs.
2. Retracement control. The stop loss is set to 150 points, which can effectively control single losses.
3. High profit-loss ratio. The take-profit is 200 points, the stop-loss is 150 points, and the profit-loss ratio is as high as 1.33, making it easy to make a profit.
4. The transaction frequency is moderate. Only trade in trending market conditions and will not enter and exit frequently.
## Risk Analysis
This strategy also has the following risks:
1. Risk of failure in trend judgment. The Ichimoku cloud indicator will generate an error signal when it fails to determine the trend change. The parameter period can be appropriately extended for optimization.
2. Risk of stop loss being exceeded. Stop loss may be breached in rapid market conditions. You can set a trailing stop or consider increasing the stop loss range.
3. Night trading and pre-market trading risks. The strategy defaults to only trading in the day session, and market judgments in night sessions and pre-market may be invalid. You can set up 24-hour trading or develop separate trading strategies before and after the market.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimization of Ichimoku cloud indicator parameters. Different conversion line, baseline and alternative line parameters can be tested to find the best parameter combination.
2. ADX parameters and threshold optimization. You can test the period parameters and filtering thresholds of ADX to find the optimal parameters.  
3. Optimize stop-profit and stop-loss. The optimal take profit and stop loss points can be determined based on historical data backtesting.
4. Trailing stop strategy. Set a floating stop to better follow the trend and take profits.
5. Auxiliary indicators for trend judgment. Add MACD, KD and other indicators to assist in judging trends and improve signal accuracy.
6. Adaptive optimization. Develop separate trading strategy parameters for widely different varieties.
## Summarize
The Ichimoku cloud quantitative short-term strategy integrates the advantages of the Ichimoku cloud indicator and the ADX indicator, which can not only accurately determine the turning point of the trend, but also effectively filter out the consolidating market and avoid false signals. This strategy has a high profit-loss ratio and controllable drawdowns, and is suitable for short-term operations following trends. Through parameter optimization, stop loss optimization, auxiliary indicators and other means, the stability and profitability of the strategy can be further improved.
||

## Overview  

The Ichimoku Cloud Quant Scalping Strategy is a short-term quantitative strategy integrating Ichimoku Cloud and Average Directional Index (ADX). It utilizes Ichimoku Cloud to determine the trend direction and ADX to filter non-trending markets for scalping during trending conditions.  

## Strategy Logic  

The strategy consists of two main components:  

1. Ichimoku Cloud to judge the trend direction  

    - Conversion Line: middle price of last 7 periods
    - Base Line: middle price of last 26 periods
    - Leading Span A: midpoint of Conversion Line and Base Line
    - Leading Span B: middle price of last 52 periods
    
    Price above the cloud indicates an uptrend while below means a downtrend. The strategy uses the breakout of Conversion Line to determine the reversal of the trend.
    
2. ADX to filter non-trending market

    Only taking signals when ADX is greater than 20, suggesting a trending market. No trade when ADX<20 during range-bound market.
    
Trade Rules:

- Long Entry: Price breaks above Conversion Line and ADX>20
- Short Entry: Price breaks below Conversion Line and ADX>20  
- Stop Loss: 150 ticks  
- Take Profit: 200 ticks

## Advantage Analysis   

The advantages of this strategy:  

1. Following the trend, avoiding ranges. Ichimoku Cloud can accurately determine trend direction and turning points. ADX filters range-bound market to prevent false breakout.  

2. Drawdown control. 150 ticks stop loss effectively limits per trade loss.

3. High profit factor. 200 ticks take profit vs 150 ticks stop loss gives a profit factor of 1.33, easy to gain profits.  

4. Appropriate trading frequency. Only trading when a trend emerges prevents over-trading.

## Risk Analysis

The risks are:

1. Trend determination failure risk. Incorrect signal when Ichimoku Cloud fails to detect trend reversal. Can optimize parameters to improve accuracy.  

2. Stop loss being hit risk. Stop loss can be penetrated during fast market. Can use trailing stop loss or wider stop loss range.

3. Overnight and premarket trading risk. Default setting only allows day trading. Judgement may fail during extended hours. Can enable 24H trading or customize strategies for extended sessions.

## Optimization Directions 

The potential optimization directions:  

1. Parameter tuning of Ichimoku Cloud to find the optimal setting.
  
2. ADX parameter and threshold optimization to determine the best values.
  
3. Profit target and stop loss optimization based on historical data.

4. Trailing stop loss to better follow the trend.  

5. Additional indicators like MACD and KD to assist trend determination.

6. Adaptive optimization for different products.
   
## Conclusion
  
The Ichimoku Cloud Quant Scalping Strategy integrates the advantages of Ichimoku Cloud and ADX to accurately determine trend reversal points and filter out range-bound markets. It has high profit factor, controllable drawdown, and is suitable for scalping along the trend. Further improvements on parameters, stop loss, auxiliary indicators can enhance the stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|7|Conversion Periods:|
|v_input_2|14|Length|
|v_input_3|20|threshold|
|v_input_4|true|Use Trading Session?|
|v_input_5|0400-1500|Trade Session:|
|v_input_6|true|Trade Size:|
|v_input_7|150|Stop Loss in ticks:|
|v_input_8|200|Take Profit in ticks:|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-13 00:00:00
end: 2023-12-20 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title='[STRATEGY][RS]Spot/Binary Scalper V0', shorttitle='IC', overlay=true, initial_capital=100000, currency=currency.USD)
//  ||  Adapted from:
//  ||      http://www.binaryoptionsedge.com/topic/1414-ta-spot-scalping-it-works-damn-good/?hl=singh

//  ||  Ichimoku cloud:
conversionPeriods = input(title='Conversion Periods:',  defval=7, minval=1),
basePeriods = 26//input(title='Base Periods',  defval=26, minval=1)
laggingSpan2Periods = 52//input(title='Lagging Span:',  defval=52, minval=1),
displacement = 26//input(title='Displacement:',  defval=26, minval=1)

f_donchian(_len) => avg(lowest(_len), highest(_len))

f_ichimoku_cloud(_conversion_periods, _base_periods, _lagging_span)=>
    _conversion_line = f_donchian(_conversion_periods)
    _base_line = f_donchian(_base_periods)
    _lead_line1 = avg(_conversion_line, _base_line)
    _lead_line2 = f_donchian(_lagging_span)
    [_conversion_line, _base_line, _lead_line1, _lead_line2]

[conversionLine, baseLine, leadLine1, leadLine2] = f_ichimoku_cloud(conversionPeriods, basePeriods, laggingSpan2Periods)

//ps0 = plot(title='A', series=leadLine1, color=green, linewidth=2)
//ps1 = plot(title='B', series=leadLine2, color=red, linewidth=2)
//fill(title='AB', plot1=ps0, plot2=ps1, color=blue, transp=80)
//plot(title='Base', series=baseLine, color=blue, linewidth=1, offset=displacement)
plot(title='Conversion', series=conversionLine, color=blue, linewidth=1)
//  ||----------------------------------------------------------------------------------------------------------------------------------------------||
//  ||  ADX
len = input(title="Length",  defval=14)
th = input(title="threshold",  defval=20)

TrueRange = max(max(high-low, abs(high-nz(close[1]))), abs(low-nz(close[1])))
DirectionalMovementPlus = high-nz(high[1]) > nz(low[1])-low ? max(high-nz(high[1]), 0): 0
DirectionalMovementMinus = nz(low[1])-low > high-nz(high[1]) ? max(nz(low[1])-low, 0): 0


SmoothedTrueRange = nz(SmoothedTrueRange[1]) - (nz(SmoothedTrueRange[1])/len) + TrueRange
SmoothedDirectionalMovementPlus = nz(SmoothedDirectionalMovementPlus[1]) - (nz(SmoothedDirectionalMovementPlus[1])/len) + DirectionalMovementPlus
SmoothedDirectionalMovementMinus = nz(SmoothedDirectionalMovementMinus[1]) - (nz(SmoothedDirectionalMovementMinus[1])/len) + DirectionalMovementMinus

DIPlus = SmoothedDirectionalMovementPlus / SmoothedTrueRange * 100
DIMinus = SmoothedDirectionalMovementMinus / SmoothedTrueRange * 100
DX = abs(DIPlus-DIMinus) / (DIPlus+DIMinus)*100
ADX = sma(DX, len)
//  ||----------------------------------------------------------------------------------------------------------------------------------------------||
//  ||  Trade session:
USE_TRADESESSION = input(title='Use Trading Session?', type=bool, defval=true)
trade_session = input(title='Trade Session:', defval='0400-1500', confirm=false)
istradingsession = not USE_TRADESESSION ? false : not na(time('1', trade_session))
bgcolor(istradingsession?gray:na)
//  ||----------------------------------------------------------------------------------------------------------------------------------------------||
//  ||  Strategy:
trade_size = input(title='Trade Size:',  defval=1)
stop_loss_in_ticks = input(title='Stop Loss in ticks:',  defval=150)
take_profit_in_ticks = input(title='Take Profit in ticks:',  defval=200)

buy_icloud_signal = open < conversionLine and close > conversionLine
buy_adx_signal = DIPlus > 20
buy_signal = istradingsession and buy_icloud_signal and buy_adx_signal

sel_icloud_signal = open > conversionLine and close < conversionLine
sel_adx_signal = DIMinus > 20
sel_signal = istradingsession and sel_icloud_signal and sel_adx_signal


strategy.order('buy', long=true, qty=trade_size, comment='buy', when=buy_signal)
strategy.order('sel', long=false, qty=trade_size, comment='sel', when=sel_signal)

strategy.exit('exit buy', from_entry='buy', profit=take_profit_in_ticks, loss=stop_loss_in_ticks)
strategy.exit('exit sel', from_entry='sel', profit=take_profit_in_ticks, loss=stop_loss_in_ticks)

```

> Detail

https://www.fmz.com/strategy/436096

> Last Modified

2023-12-21 11:13:15
