
> Name

MA-and-MA-Crossover-Trading-Strategy-Based-on-FRAMA-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1dce7da36148dd86acd.png)
 [trans]

## Overview
This strategy first calculates the fast moving average ma_fast and the slow moving average ma_slow, and then combines the FRAMA adaptive moving average to go long when ma_fast crosses above ma_slow, and close the position when ma_slow crosses below ma_fast or when FRAMA crosses below the closing price.
## Strategy Principle
1. Calculate the 13-day simple moving average ma_fast and the 26-day simple moving average ma_slow.
2. Calculate the FRAMA adaptive moving average out. The calculation formula of FRAMA is more complicated. The main idea is to dynamically adjust the smoothness α of the moving average based on the highest value, lowest value and volatility of the price.
3. Go long when ma_fast wears ma_slow. This means that the short-term moving average begins to rise and outperforms the long-term moving average, which is in line with the characteristics of the trend.
4. Close the position when ma_slow crosses below ma_fast or when FRAMA crosses below the closing price. This indicates a trend reversal signal.
## Advantage Analysis
1. Combine the advantages of the dual moving average system and the adaptive moving average system. The dual moving average system is good at capturing trends, and the adaptive moving average system can better filter out noise.
2. The FRAMA indicator can automatically adjust parameters to avoid the subjectivity of manual parameter selection.
3. Use two exit signals at the same time to catch trend reversals in time.
## Risk Analysis
1. There is a possibility of dislocation when the double moving average crosses, which may result in intermittent losses.
2. The adaptive moving average will increase the number of parameters of the strategy and may lead to over-optimization.
3. Only considering price factors without filtering based on transaction volume, you may miss opportunities.

## Optimization direction
1. You can test moving average combinations of different periods to find the best parameters.
2. You can add confirmation of trading volume to avoid invalid signals. For example, add conditions for a sudden increase in trading volume.
3. The conditions for opening and closing positions can be optimized to make the strategy more stable. For example, only open a position on a breakout of a continuation pattern.

## Summarize
This strategy combines double moving average crossovers and FRAMA adaptive moving averages to automatically adapt to the market environment by dynamically adjusting parameters. Double moving averages are good at capturing trends, and FRAMA can filter out noise. Using two closing signals at the same time makes the strategy more robust. The next step can be to further optimize the parameters and add confirmation of trading volume to make the strategy more complete.
|| 

# Summary

This strategy calculates the fast moving average line ma_fast and slow moving average line ma_slow first, and then combines with the FRAMA adaptive moving average line. It goes long when ma_fast crosses over ma_slow, and closes position when ma_slow crosses below ma_fast or FRAMA falls below close price.

# Strategy Logic

1. Calculate the 13-day simple moving average ma_fast and 26-day simple moving average ma_slow. 

2. Calculate the FRAMA adaptive moving average line out. The FRAMA formula is complex, the main idea is to dynamically adjust the smoothness α of the moving average based on the highest, lowest and volatility of prices.

3. Go long when ma_fast crosses over ma_slow. This indicates the short-term moving average starts to move up and runs faster than the long-term one, matching the trending characteristics.  

4. Close position when ma_slow crosses below ma_fast or FRAMA falls below close price. These indicate trend reversal signals.

# Advantage Analysis

1. Combines the advantages of dual moving average system and adaptive moving average system. Dual MA system is good at catching trends, while adaptive MA system filters out noises better.

2. FRAMA indicator automatically adjusts parameters, avoiding the subjectivity of manual parameter tuning.

3. Using two exit signals enables timely catching trend reversals. 

# Risk Analysis

1. Dual moving average crossovers can have whipsaws, resulting in intermittent losses.

2. Adaptive moving averages introduce more parameters, risking overfitting. 

3. Only considers price factors without trading volume filter, hence may miss opportunities.

# Optimization

1. Test different MA periods to find the optimal combination.  

2. Add volume confirmation to avoid false signals, e.g. requiring volume spikes.

3. Optimize entry and exit rules to make the strategy more robust, e.g. only taking signals in continuation patterns.


# Conclusion

This strategy combines dual moving average crossover and FRAMA adaptive moving average, automatically adapting to market conditions by dynamically adjusting parameters. Dual MAs are good at catching trends while FRAMA filters out noises. Using two exit signals also makes the strategy more robust. Next steps could be further parameter optimization and adding volume filter to improve it.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hl2|0|price: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_2|16|len|
|v_input_3|true|FC|
|v_input_4|198|SC|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-14 00:00:00
end: 2024-01-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Fractal Adaptive Moving Average",shorttitle="FRAMA",overlay=true)


ma_fast = sma(close,13)

ma_slow = sma(close,26)
plot(ma_fast,color = green)
plot(ma_slow, color = yellow)
price = input(hl2)
len = input(defval=16,minval=1)
FC = input(defval=1,minval=1)
SC = input(defval=198,minval=1)
len1 = len/2
w = log(2/(SC+1))
H1 = highest(high,len1)
L1 = lowest(low,len1)
N1 = (H1-L1)/len1
H2 = highest(high,len)[len1]
L2 = lowest(low,len)[len1]
N2 = (H2-L2)/len1
H3 = highest(high,len)
L3 = lowest(low,len)
N3 = (H3-L3)/len
dimen1 = (log(N1+N2)-log(N3))/log(2)
dimen = iff(N1>0 and N2>0 and N3>0,dimen1,nz(dimen1[1]))
alpha1 = exp(w*(dimen-1))
oldalpha = alpha1>1?1:(alpha1<0.01?0.01:alpha1)
oldN = (2-oldalpha)/oldalpha
N = (((SC-FC)*(oldN-1))/(SC-1))+FC
alpha_ = 2/(N+1)
alpha = alpha_<2/(SC+1)?2/(SC+1):(alpha_>1?1:alpha_)
out = (1-alpha)*nz(out[1]) + alpha*price
plot(out,title="FRAMA",color=purple,transp=0)
entry() => crossover(ma_fast, ma_slow) and (out < close)
exit() => crossover(ma_slow, ma_fast) or crossunder(out, close)

strategy.entry(id= "MA cross", long = true, when = entry())
strategy.close(id= "MA cross", when = exit())
```

> Detail

https://www.fmz.com/strategy/438806

> Last Modified

2024-01-15 14:38:48
