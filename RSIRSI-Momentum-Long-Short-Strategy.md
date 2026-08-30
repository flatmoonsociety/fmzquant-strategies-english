
> Name

RSI Long-Short Momentum Strategy RSI-Momentum-Long-Short-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9e2036cdbcd46ede7f7105c78a4a76d4f65fbd54b2af3678995943f3c3db904b.png)

[trans]

## Overview
The RSI long-short momentum strategy is a typical momentum strategy based on the Larry Connors RSI indicator, which uses the overbought and oversold signals of the RSI indicator to determine buying and selling. This strategy mainly determines whether the price is overbought or oversold, and uses this as a buy or sell signal.
## Strategy Principle
This strategy constructs the RSI indicator by calculating upward and downward price momentum over a period of time. When the RSI indicator is below the oversold line of 10, it is considered oversold, and when the indicator is above the overbought line of 90, it is considered overbought. The strategy generates a buy signal when the RSI indicator crosses the oversold line from a low level, and a sell signal when the RSI indicator crosses the overbought line from a high level.
The strategy adds an additional moving average judgment rule, which requires that a buy signal can be generated when the 5-day moving average is higher than the 200-day moving average, and a sell signal can be generated when the 5-day moving average is lower than the 200-day moving average. This can filter out false signals caused by short-term rebounds.
In addition, the strategy also adds a profit-taking mechanism. When holding a long position, if the RSI indicator crosses the overbought line of 90, all long positions will be forced to be closed; when holding a short position, if the RSI indicator crosses the oversold line of 10, all short positions will be forced to be closed. This can lock in profits and avoid losses from expanding.
## Strategic Advantages
1. Use the RSI indicator to determine overbought and oversold conditions and capture the opportunity for price reversal.
2. Adding moving average filtering can reduce erroneous transactions caused by short-term noise.
3. Set up a profit-taking mechanism to control risks and avoid losses from expanding.
4. The policy rules are simple and clear, easy to understand and implement.
5. RSI is a commonly used and practical technical indicator, applicable to many stocks and digital currencies.
## Strategy Risk
1. The RSI indicator may fail to reverse. Price overbought or oversold does not necessarily lead to a reversal.
2. Moving average filtering may also filter out better trading opportunities.
3. Improper take-profit setting will also result in premature take-profit, making it impossible to hold the long-term trend.
4. Parameters need to be adjusted appropriately, such as calculating the cycle length of RSI, overbought and oversold thresholds, moving average parameters, etc.
The above risks can be reduced by optimizing parameters, combining other indicators, and appropriately loosening the profit limit.
## Strategy optimization direction
1. You can test the effects of RSI indicators in different periods.
2. You can add other indicators, such as KDJ, MACD, etc. to form a combination with RSI.
3. The overbought and oversold thresholds can be adjusted according to market conditions.
4. The RSI value for take profit activation can be adjusted according to the specific position holding time.
5. You can add a stop loss strategy to stop the loss when the loss reaches a certain proportion.
6. The moving average system can be optimized and changed to dynamic tracking stop loss.
## Summarize
The RSI long-short momentum strategy uses the RSI indicator to determine overbought and oversold conditions as signals, and adds moving averages and take-profit rules for filtering, which can effectively seize short-term reversal opportunities. This strategy is simple and practical, and deserves further testing and optimization to adapt to a wider range of market conditions. Overall, this strategy provides a good idea and can be used as a reference for the development of quantitative trading strategies.
|| 


## Overview

The RSI Momentum Long Short strategy is a typical momentum strategy based on the Larry Connors RSI indicator, using the overbought and oversold signals from RSI to determine entries and exits. The key is to identify whether the price is in overbought or oversold status and use that as trading signals.

## Strategy Logic

The strategy constructs RSI indicator by calculating the upside momentum and downside momentum of prices over a lookback period. RSI below oversold line 10 is considered oversold, while RSI above overbought line 90 is considered overbought. The strategy generates long signals when RSI crosses oversold line from below, and generates short signals when RSI crosses overbought line from above.

Additional moving average filters are added - only allowing long signals when 5day MA is above 200day MA, and short signals when 5day MA is below 200day MA. This helps filter out false signals from short-term rebounds. 

Profit taking mechanisms are also introduced. Existing long positions will be closed out when RSI crosses above overbought line 90. Existing short positions will be closed out when RSI crosses below oversold line 10. This locks in profits and avoids increasing losses.

## Advantages of the Strategy

1. Using RSI to identify overbought/oversold levels catches price reversal moments. 

2. Adding MA filters reduces false signals from short-term noise.

3. Profit-taking mechanics help control risks and limit losses.

4. Simple and clear rules, easy to understand and implement.

5. RSI is a widely used and practical indicator, suitable for many instruments.

## Risks of the Strategy

1. RSI overbought/oversold may not always result in reversal.

2. MA filters could also filter out good trading opportunities. 

3. Improper profit-taking settings give up trends too early.

4. Parameters like RSI lookback, overbought/oversold levels, MA settings need tuning.

Risks can be reduced via parameter optimization, combining other indicators, flexible profit-taking, etc.

## Enhancement Opportunities 

1. Test RSI with different lookback periods.

2. Add other indicators like KDJ, MACD to supplement RSI. 

3. Adjust overbought/oversold levels based on market regimes.

4. Fine tune profit-taking RSI levels based on holding period.

5. Incorporate stop loss strategies based on max loss percentage.

6. Optimize MA system, use dynamic trailing stop loss.

## Conclusion

The RSI Momentum Long Short Strategy catches short-term reversal opportunities by using RSI to identify overbought/oversold levels, filtered by MAs and profit-taking rules. The strategy is simple and practical, worth further testing and enhancement to adapt to diverse markets. Overall it provides a good framework that can serve as a reference for quantitative trading strategy development.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Entry area|
|v_input_2|90|overBought|
|v_input_3|10|overSold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-25 00:00:00
end: 2023-10-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//authour: SudeepBisht
//@version=3
//Based on Larry Connors RSI-2 Strategy - Lower RSI
strategy("SB_CM_RSI_2_Strategy_Version 2.0", overlay=true)

src = close
entry= input(defval=0,title="Entry area")
entry:=nz(entry[1])
overBought=input(90)
overSold=input(10)
//RSI CODE
up = rma(max(change(src), 0), 2)
down = rma(-min(change(src), 0), 2)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
//Criteria for Moving Avg rules
ma5 = sma(close,5)
ma200= sma(close, 200)

//Rule for RSI Color
col = close > ma200 and close < ma5 and rsi < 10 ? lime : close < ma200 and close > ma5 and rsi > 90 ? red : silver
chk= col==red?-1:col==lime?1:0

if (not na(rsi))
    if (crossover(rsi, overSold))
        if(chk[1]==1)
            strategy.entry("RsiLE", strategy.long, comment="RsiLE")
            entry:=1
    if (crossunder(rsi, overBought))
        if(chk[1]==-1)
            strategy.entry("RsiSE", strategy.short, comment="RsiSE")
            entry:=-1
        
if (not na(rsi))
    if (crossover(rsi, overSold) and entry==-1)
        strategy.close_all()
        //strategy.entry("RsiLE", strategy.long, comment="RsiLE")
        entry:=0
    if (crossunder(rsi, overBought) and entry==1)
        strategy.close_all()
        //strategy.entry("RsiSE", strategy.short, comment="RsiSE")
        entry:=0
        

```

> Detail

https://www.fmz.com/strategy/430271

> Last Modified

2023-10-26 17:05:40
