
> Name

Multi-Timeframe-RSI-EMA-Momentum-Trading-Strategy-with-Position-Scaling
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b7fa6b4c61644cfc95.png)

[trans]
#### Overview
This is a momentum trading strategy based on RSI and EMA indicators, which combines multiple time period technical analysis methods. This strategy trades through RSI overbought and oversold signals and EMA trend confirmation, and uses a dynamic position adjustment mechanism. The core of the strategy is to combine the signals of short-term RSI (2 periods) and medium-term RSI (14 periods), and use three EMAs (50/100/200) of different periods to confirm the market trend direction.
#### Strategy Principle
The strategy uses a multi-layer verification mechanism for trading decisions. Long conditions require RSI14 to be below 31 and RSI2 to break through 10 upwards, and EMA50, EMA100, and EMA200 to be in a short position. The short selling conditions require RSI14 to be higher than 69 and RSI2 to fall below 90. It also requires EMA50, EMA100, and EMA200 to be arranged in a long position. The strategy also includes a take-profit mechanism based on the RSI indicator, which automatically closes positions when RSI reaches an extreme value and the price is favorable for the position. What's special is that the strategy adopts a dynamic position management system based on account equity. Each time a position is opened, the appropriate position size will be calculated based on the current equity.
#### Strategic Advantages
1. The signal confirmation mechanism is perfect and the risk of false signals is reduced through multiple technical indicator verifications.
2. The dynamic position management system can automatically adjust the trading volume according to the account size
3. Use RSI of different periods to confirm the trend of EMA to improve the accuracy of trading.
4. Have a clear profit-taking mechanism and be able to lock in profits in a timely manner
5. The strategy has good visualization effects, making it easier for traders to understand the market status.
6. Using a layered combination of technical indicators can better capture changes in market momentum.
#### Strategy Risk
1. High leverage (20 times) may lead to greater account fluctuations
2. Frequent false breakthrough signals may occur in sideways markets
3. The position doubling mechanism may aggravate losses in the event of continuous losses.
4. There is no stop-loss mechanism, which may cause large losses in extreme market conditions.
5. EMA trend judgment may lag when the market turns rapidly
6. The RSI indicator can produce misleading signals under certain market conditions.
#### Strategy optimization direction
1. Introduce a dynamic stop loss mechanism, which can set stop loss points based on ATR or volatility
2. Optimize the position management system and set maximum position limits to control risks
3. Add market volatility filter to adjust trading parameters in high volatility environment
4. Consider adding a time filter to avoid trading during unfavorable times
5. Introduce more market status judgment indicators, such as trading volume indicators
6. Develop an adaptive parameter system to dynamically adjust indicator parameters according to the market environment
#### Summary
This is a strategy that combines the characteristics of momentum trading and trend following, and improves the reliability of trading through the combined use of multiple technical indicators. Although there are some risk points, the stability of the strategy can be further improved through the suggested optimization directions. The biggest feature of the strategy is that it combines short-term and medium-term technical indicators with dynamic position management to form a complete trading system. Through reasonable risk management and parameter optimization, this strategy is expected to achieve stable performance in actual transactions. ||
#### Overview
This is a momentum trading strategy based on RSI and EMA indicators, combining technical analysis across multiple timeframes. The strategy executes trades based on RSI overbought/oversold signals with EMA trend confirmation and employs dynamic position sizing. The core concept lies in combining short-term RSI (2-period) with medium-term RSI (14-period) signals, while using three different period EMAs (50/100/200) for trend direction confirmation.

#### Strategy Principles
The strategy employs a multi-layer validation mechanism for trading decisions. Long conditions require RSI14 below 31 and RSI2 crossing above 10, along with EMA50, EMA100, and EMA200 in bearish alignment. Short conditions require RSI14 above 69 and RSI2 crossing below 90, with EMAs in bullish alignment. The strategy includes an RSI-based take-profit mechanism, automatically closing positions when RSI reaches extreme values and price movement favors the position. A notable feature is the dynamic position sizing system based on account equity, calculating appropriate position sizes for each trade.

#### Strategy Advantages
1. Comprehensive signal confirmation mechanism reduces false signal risks through multiple technical indicator validation
2. Dynamic position sizing system automatically adjusts trading volume based on account size
3. Multiple period RSI combined with EMA trend confirmation improves trading accuracy
4. Clear take-profit mechanism ensures timely profit capture
5. Excellent visualization features help traders understand market conditions
6. Layered technical indicator combination better captures market momentum changes

#### Strategy Risks
1. High leverage (20x) may lead to significant account volatility
2. May generate frequent false breakout signals in ranging markets
3. Position multiplication mechanism could amplify losses during consecutive losing trades
4. Lack of stop-loss mechanism might result in substantial losses in extreme market conditions
5. EMA trend judgment may lag during rapid market reversals
6. RSI indicators might generate misleading signals under certain market conditions

#### Strategy Optimization Directions
1. Introduce dynamic stop-loss mechanism based on ATR or volatility
2. Optimize position management system with maximum position limits for risk control
3. Add volatility filters to adjust trading parameters in high volatility environments
4. Consider implementing time filters to avoid unfavorable trading periods
5. Incorporate additional market state indicators, such as volume indicators
6. Develop adaptive parameter system to dynamically adjust indicator parameters based on market conditions

#### Summary
This strategy combines momentum trading with trend following characteristics, enhancing trading reliability through multiple technical indicators. While certain risks exist, the suggested optimization directions can further improve strategy stability. The strategy's main feature is the combination of short-term and medium-term technical indicators with dynamic position management, forming a complete trading system. Through proper risk management and parameter optimization, this strategy shows promise for stable performance in actual trading.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-21 00:00:00
end: 2024-11-28 00:00:00
period: 15m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Custom RSI EMA Strategy", overlay=true, default_qty_type=strategy.fixed, default_qty_value=1)

// Definování vstupních podmínek
rsi_14 = ta.rsi(close, 14)
rsi_2 = ta.rsi(close, 2)
ema_50 = ta.ema(close, 50)
ema_100 = ta.ema(close, 100)
ema_200 = ta.ema(close, 200)

// Pákový efekt
leverage = 20

// Podmínky pro long pozici
longCondition = (rsi_14[1] < 31) and ta.crossover(rsi_2, 10) and (ema_50 < ema_100) and (ema_100 < ema_200)

// Podmínky pro short pozici
shortCondition = (rsi_14[1] > 69) and ta.crossunder(rsi_2, 90) and (ema_50 > ema_100) and (ema_100 > ema_200)

// Definování průměrné ceny pozice
var float long_avg_price = na
var float short_avg_price = na

// Sledujeme, zda se velikost pozice změnila
var float last_position_size = na

// Přerušení průměrné ceny pozice při změně pozice
if (last_position_size != strategy.position_size)
    long_avg_price := na
    short_avg_price := na

// Aktualizace průměrné ceny pozice
if (strategy.position_size > 0)
    long_avg_price := strategy.position_avg_price
    short_avg_price := na
else if (strategy.position_size < 0)
    short_avg_price := strategy.position_avg_price
    long_avg_price := na

// Uložení aktuální velikosti pozice pro příští bar
last_position_size := strategy.position_size

// Podmínky pro take profit
takeProfitLongCondition = (rsi_14 > 69) and (rsi_2 > 90) and (long_avg_price < close)
takeProfitShortCondition = (rsi_14 < 31) and (rsi_2 < 10) and (short_avg_price > close)

// Velikost pozice
new_position_size = strategy.position_size == 0 ? na : math.abs(strategy.position_size) * 2

// Úprava velikosti pozice s ohledem na pákový efekt
position_value = strategy.equity * leverage
trade_qty = position_value / close

// Vstup do long pozice s dvojnásobkem aktuální pozice nebo standardní velikostí při první pozici
if (longCondition)
    strategy.entry("Long", strategy.long, qty=new_position_size == na ? trade_qty : new_position_size)

// Vstup do short pozice s dvojnásobkem aktuální pozice nebo standardní velikostí při první pozici
if (shortCondition)
    strategy.entry("Short", strategy.short, qty=new_position_size == na ? trade_qty : new_position_size)

// Výstup z long pozice při splnění podmínek pro take profit
if (takeProfitLongCondition)
    strategy.close("Long")

// Výstup z short pozice při splnění podmínek pro take profit
if (takeProfitShortCondition)
    strategy.close("Short")

// Zvýraznění části grafu, kde platí podmínky pro long
highlightLongCondition = (ema_50 < ema_100) and (ema_100 < ema_200)
bgcolor(highlightLongCondition ? color.new(color.green, 90) : na)

// Zvýraznění části grafu, kde platí podmínky pro short
highlightShortCondition = (ema_50 > ema_100) and (ema_100 > ema_200)
bgcolor(highlightShortCondition ? color.new(color.red, 90) : na)

// Přidání bodů pozic do grafu
plotshape(series=longCondition, location=location.belowbar, color=color.green, style=shape.labelup, text="L")
plotshape(series=shortCondition, location=location.abovebar, color=color.red, style=shape.labeldown, text="S")

// Vykreslení průměrné ceny pozice pro long a short
plot(long_avg_price, title="Long Avg Price", color=color.blue, linewidth=2)
plot(short_avg_price, title="Short Avg Price", color=color.orange, linewidth=2)
```

> Detail

https://www.fmz.com/strategy/473361

> Last Modified

2024-11-29 15:23:44
