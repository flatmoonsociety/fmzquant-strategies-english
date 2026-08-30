
> Name

Significant-Pivot-Points-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ce944a720ed9db1712.png)
[trans]
### Overview
This strategy is optimized based on the traditional pivot point reversal strategy. It mainly calculates ATR and sets the ATR filter factor to filter out some meaningless pivot points and only trade those truly important pivot points.
### Strategy Principles
The core logic of this strategy is to calculate important pivot highs and pivot lows. The main steps in calculating the pivot high are:
1. Calculate ATR and set the ATR filter factor atr_mult.
2. Traverse a certain number of K lines on the left (set by leftBars). If the high point fulcrum is higher than the high point + ATR*atr_mult of any left K line, the fulcrum is invalid.
3. Traverse a certain number of K lines on the right (set by rightBars). If the high point fulcrum is higher than the high point + ATR*atr_mult of any right K line, the fulcrum is invalid.
4. If the high point pivot is still valid after the above test, return the high point as an important high point pivot point.
The logic for calculating pivot lows is similar.
After obtaining an important pivot point, when the price breaks through the important high point pivot point, go short; when the price breaks through the important low point pivot point, go long.
### Advantage Analysis
The main advantages of this strategy are:
1. Through the ATR and atr_mult filter parameters, you can filter out meaningless small fluctuations and only trade the truly important pivot points to avoid unnecessary transactions.
2. The ATR parameter can be dynamically adjusted to automatically adjust the trading range in a volatile market to avoid over-trading.
3. The pivot reversal strategy itself has a relatively high winning rate and profit rate.
### Risk Analysis
The main risks of this strategy are:
1. Improper setting of ATR parameters may filter out too many effective trading opportunities. If the ATR is too large, valid pivot points may also be filtered.
2. The fulcrum reversal strategy itself still has the risk of being stuck, and stop loss needs to be set to control the risk.
3. Reversal strategies are sensitive to transaction costs and require reasonable stop loss and take profit settings.
In order to control the above risks, optimization can be carried out from the following aspects:
1. Optimize ATR parameters to ensure sufficient trading opportunities.
2. Set a reasonable stop loss and take profit ratio.
3. Appropriately adjust the opening lot size to reduce the impact of transaction costs.
### Optimization direction
This strategy can also be further optimized from the following directions:
1. Combine with other indicators to determine the market trend status and avoid reversal transactions in trending markets. You can consider adding MACD, KDJ and other indicators.
2. Add machine learning algorithm to automatically optimize parameters. You can use genetic algorithm, random forest and other methods to find the optimal parameter combination.
3. Add quantitative data for training to find the best ATR range. Adding historical data can improve the accuracy of parameter selection.
4. You can consider using it in combination with other strategies to combine the advantages of different types of strategies. For example, combined with the trend following strategy, it can reverse during consolidation and follow the trend.
### Summarize
This important pivot point reversal strategy filters out meaningless small fluctuations by calculating ATR and setting filter factors, and only conducts reversal transactions at important pivot points, which can effectively improve the profitability of the strategy. At the same time, it also increases the difficulty of parameter optimization. It is necessary to comprehensively consider multiple aspects such as ATR range, stop loss and take profit ratio to find the optimal parameters. If the parameters are optimized in place, this strategy can become an efficient and stable short-term trading strategy.
||

### Overview  

This strategy optimizes the traditional pivot points reversal strategy by calculating the ATR and setting ATR filters to eliminate insignificant pivot points, only trading on truly significant ones.   

### Strategy Logic  

The core logic is to identify significant peak and trough pivot points. The key steps to calculate significant peak pivots are:

1. Calculate ATR and set the ATR filter factor atr_mult. 
2. Traverse a certain number of bars on the left (set by leftBars), if the peak pivot is higher than any high + ATR*atr_mult on the left, the pivot is invalid.
3. Traverse a certain number of bars on the right (set by rightBars), if the peak pivot is higher than any high + ATR*atr_mult on the right, the pivot is invalid.  
4. If the peak pivot remains valid after the above tests, return it as an important peak pivot.

The logic for calculating significant trough pivots is similar.  

After obtaining the significant pivots, go short when price breaks an important peak pivot, and go long when it breaks an important trough pivot.

### Advantage Analysis   

The main advantages of this strategy are:  

1. The ATR and atr_mult filter can eliminate insignificant fluctuations and only trade truly significant pivots, avoiding unnecessary trades.  
2. The dynamic ATR parameter can adjust the trading range automatically in volatile markets, preventing over-trading.
3. Pivot points reversal itself has relatively high win rate and profitability.  

### Risk Analysis   

The main risks are:   

1. Improper ATR parameters may filter out too many valid trades. If ATR is too high, valid pivots could be eliminated.  
2. Risk of being trapped still exists, need to set stop loss to control risk.  
3. Reversal strategies are sensitive to transaction costs, reasonable stop loss and take profit should be set.  

To control the above risks, optimize from the following aspects:
1. Optimize ATR parameters to ensure enough trading opportunities.  
2. Set reasonable stop loss and take profit ratios.
3. Adjust position sizing to reduce transaction cost impact.  

### Optimization Directions   

Further optimization directions include:  

1. Combining with other indicators to determine market regime, avoiding trading reversals in trending markets. Consider MACD, KDJ etc.  

2. Adding machine learning algorithms to auto-optimize parameters. Methods like genetic algorithms, random forest can be used to find optimum parameter sets.  

3. Training models using quantitative data to find optimal ATR range. More historical data improves parameter selection accuracy.   

4. Consider combining with other strategies, utilizing strengths of different strategy types. For example, combining with trend following strategy, reverse during ranging, trend-follow during sustained trends.

### Conclusion   

This significant pivot reversal strategy filters out meaningless minor fluctuations by calculating ATR and setting filters. Only trading reversals on significant pivots can effectively improve strategy profitability. Meanwhile, it also increases parameter optimization difficulty. The optimal parameters need to be found by comprehensive consideration of ATR range, stop loss/take profit ratios etc. If optimized thoroughly, it can become a highly efficient and stable short-term trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|PP Left Bars|
|v_input_2|2|PP Right Bars|
|v_input_3|14|ATR Length|
|v_input_4|0.1|ATR Mult|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - Significant Pivot Reversal Strategy", shorttitle = "SPPS", overlay=true)

// Inputs 
leftBars   = input(4,   title = 'PP Left Bars')
rightBars  = input(2,   title = 'PP Right Bars')
atr_length = input(14,  title = 'ATR Length')
atr_mult   = input(0.1, title = 'ATR Mult')

// Pivot High Significant Function
pivotHighSig(left, right) =>
    pp_ok = true
    atr   = atr(atr_length)
    
    for i = 1 to left
        if (high[right] < high[right+i] + atr * atr_mult)
            pp_ok := false
    for i = 0 to right-1
        if (high[right] < high[i] + atr * atr_mult)
            pp_ok := false
    
    pp_ok ? high[right] : na

// Pivot Low Significant Function
pivotLowSig(left, right) =>
    pp_ok = true
    atr   = atr(atr_length)
    
    for i = 1 to left
        if (low[right] > low[right+i] - atr * atr_mult)
            pp_ok := false
    for i = 0 to right-1
        if (low[right] > low[i] - atr * atr_mult)
            pp_ok := false
    
    pp_ok ? low[right] : na


swh = pivotHighSig(leftBars, rightBars)
swl = pivotLowSig (leftBars, rightBars)

swh_cond = not na(swh)

hprice = 0.0
hprice := swh_cond ? swh : hprice[1]

le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

if (le)
    strategy.entry("PivRevLE", strategy.long, comment="PivRevLE", stop=hprice + syminfo.mintick)

swl_cond = not na(swl)

lprice = 0.0
lprice := swl_cond ? swl : lprice[1]


se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

if (se)
    strategy.entry("PivRevSE", strategy.short, comment="PivRevSE", stop=lprice - syminfo.mintick)
```

> Detail

https://www.fmz.com/strategy/440342

> Last Modified

2024-01-29 14:58:15
