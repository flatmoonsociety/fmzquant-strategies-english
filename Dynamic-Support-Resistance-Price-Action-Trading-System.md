
> Name

Dynamic-Support-Resistance-Price-Action-Trading-System-Dynamic Support Resistance Price Action Trading System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b347b8db5b73db3d44.png)

[trans]
#### Overview
This strategy is a trading system based on price action and dynamic support and resistance levels, by identifying key price patterns to trade around support and resistance levels. The system uses a 16-period dynamic support and resistance calculation method and combines four classic reversal candlestick patterns - hammer, shooting star, cross star and needle patterns to capture potential market reversal opportunities. The strategy uses fixed percentages of take-profit and stop-loss to manage risk, and sensitivity parameters to control the stringency of entry signals.
#### Strategy Principle
The core of the strategy is to dynamically calculate support and resistance levels to form an upper and lower boundary for price activity. When price approaches these key levels, the system looks for specific candlestick patterns that serve as reversal signals. Entry conditions require a reversal pattern within 1.8% of support and resistance (default sensitivity). The system uses a 35% fund management rule, combined with a 16% stop loss and a 9.5% take profit, to effectively control the risk of each transaction to about 5.6% of the total account amount. The strategy is implemented through Pine Script, which includes complete transaction management functions and visual display.
#### Strategic Advantages
1. The strategy combines the two most reliable elements in technical analysis: price patterns and support and resistance, improving the reliability of trading signals.
2. Use dynamically calculated support and resistance levels to adapt to changes in market conditions.
3. Adopt strict fund management and risk control measures to effectively prevent large drawdowns
4. The strategy logic is clear and the parameters are highly adjustable, making it easy to optimize according to different market conditions.
5. The entry signal is clear, without subjective judgment, and is suitable for automated trading.
#### Strategy Risk
1. In highly volatile markets, the effectiveness of support and resistance levels may be reduced
2. The stop loss position is relatively far away (16%), and you may suffer large losses in violent market conditions.
3. The setting of sensitivity parameters has an important impact on transaction frequency and accuracy.
4. Relying solely on price patterns may miss other important market signals
5. The impact of transaction costs on strategy returns needs to be considered
#### Strategy optimization direction
1. Introduce trading volume as an auxiliary confirmation indicator to improve signal reliability
2. Develop adaptive sensitivity parameters and dynamically adjust them according to market volatility
3. Optimize stop loss settings and consider using trailing stop loss or segmented stop loss solutions
4. Add trend filter to avoid reversal trades in strong trends
5. Develop a dynamic position management system to adjust transaction scale according to market conditions
#### Summary
This price action-based trading strategy provides traders with a systematic approach to trading by combining dynamic support and resistance levels with classic reversal patterns. The advantages of the strategy are clear logic and controllable risks, but it still needs to be continuously optimized based on actual trading results. It is recommended that traders conduct sufficient backtesting and parameter optimization before using it in real trading, and make personalized adjustments to the strategy based on market experience. ||
#### Overview
This strategy is a trading system based on price action and dynamic support/resistance levels, executing trades near key price levels when specific candlestick patterns emerge. The system utilizes a 16-period dynamic support/resistance calculation method, combined with four classic reversal candlestick patterns - Hammer, Shooting Star, Doji, and Pin Bar to capture potential market reversals. The strategy employs fixed percentage take-profit and stop-loss levels for risk management and uses a sensitivity parameter to control entry signal strictness.

#### Strategy Principles
The core of the strategy lies in dynamically calculating support and resistance levels to establish price movement boundaries. When price approaches these key levels, the system looks for specific candlestick patterns as reversal signals. Entry conditions require pattern formation within 1.8% (default sensitivity) of support/resistance levels. The system implements a 35% equity management rule with 16% stop-loss and 9.5% take-profit, effectively controlling risk at around 5.6% of total equity per trade. The strategy is implemented in Pine Script with complete trade management functionality and visualization.

#### Strategy Advantages
1. Combines two most reliable elements of technical analysis: price patterns and support/resistance, enhancing signal reliability
2. Uses dynamically calculated support/resistance levels, adapting to changing market conditions
3. Implements strict money management and risk control measures to prevent significant drawdowns
4. Clear strategy logic with adjustable parameters, facilitating optimization for different market conditions
5. Clear entry signals without subjective judgment, suitable for automated trading

#### Strategy Risks
1. Support/resistance effectiveness may decrease in highly volatile markets
2. Relatively wide stop-loss (16%) may lead to significant losses in volatile conditions
3. Sensitivity parameter settings significantly impact trading frequency and accuracy
4. Relying solely on price patterns may miss other important market signals
5. Need to consider trading costs' impact on strategy returns

#### Optimization Directions
1. Introduce volume as a confirmation indicator to improve signal reliability
2. Develop adaptive sensitivity parameters that adjust dynamically based on market volatility
3. Optimize stop-loss settings, consider implementing trailing stops or stepped stop-loss plans
4. Add trend filters to avoid reversal trades during strong trends
5. Develop dynamic position sizing system adjusting trade size based on market conditions

#### Summary
This price action-based trading strategy provides traders with a systematic trading approach by combining dynamic support/resistance levels with classic reversal patterns. The strategy's strengths lie in its clear logic and controllable risk, though continuous optimization based on actual trading results is necessary. Traders are advised to conduct thorough backtesting and parameter optimization before live trading, and customize the strategy based on market experience.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-26 00:00:00
end: 2024-12-03 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © felipemiransan

//@version=5
strategy("Price Action Strategy", overlay=true)

// Settings
length = input.int(16, title="Support and Resistance Length")
sensitivity = input.float(0.018, title="Sensitivity")

// Stop Loss and Take Profit
stop_loss_pct = input.float(16, title="Stop Loss percentage", minval=0.1) / 100
take_profit_pct = input.float(9.5, title="Take Profit percentage", minval=0.1) / 100

// Function to identify a Hammer
isHammer() =>
    body = close - open
    price_range = high - low
    lower_shadow = open - low
    upper_shadow = high - close
    body > 0 and lower_shadow > body * 2 and upper_shadow < body * 0.5 and price_range > 0

// Function to identify a Shooting Star
isShootingStar() =>
    body = open - close
    price_range = high - low
    lower_shadow = close - low
    upper_shadow = high - open
    body > 0 and upper_shadow > body * 2 and lower_shadow < body * 0.5 and price_range > 0

// Function to identify a Doji
isDoji() =>
    body = close - open
    price_range = high - low
    math.abs(body) < (price_range * 0.1)  // Doji has a small body

// Function to identify a Pin Bar
isPinBar() =>
    body = close - open
    price_range = high - low
    lower_shadow = open - low
    upper_shadow = high - close
    (upper_shadow > body * 2 and lower_shadow < body * 0.5) or (lower_shadow > body * 2 and upper_shadow < body * 0.5)

// Support and resistance levels 
support = ta.lowest(low, length)
resistance = ta.highest(high, length)

// Entry criteria
long_condition = (isHammer() or isDoji() or isPinBar()) and close <= support * (1 + sensitivity)
short_condition = (isShootingStar() or isDoji() or isPinBar()) and close >= resistance * (1 - sensitivity)

// Function to calculate stop loss and take profit (long)
calculate_levels(position_size, avg_price, stop_loss_pct, take_profit_pct) =>
    stop_loss_level = avg_price * (1 - stop_loss_pct)
    take_profit_level = avg_price * (1 + take_profit_pct)
    [stop_loss_level, take_profit_level]

// Function to calculate stop loss and take profit (short)
calculate_levels_short(position_size, avg_price, stop_loss_pct, take_profit_pct) =>
    stop_loss_level = avg_price * (1 + stop_loss_pct)
    take_profit_level = avg_price * (1 - take_profit_pct)
    [stop_loss_level, take_profit_level]

// Buy entry order with label
if (long_condition and strategy.opentrades == 0)
    strategy.entry("Buy", strategy.long)
    pattern = isHammer() ? "Hammer" : isDoji() ? "Doji" : isPinBar() ? "Pin Bar" : ""
    label.new(x=bar_index, y=low, text=pattern, color=color.green, textcolor=color.black, size=size.small)

// Sell entry order with label
if (short_condition and strategy.opentrades == 0)
    strategy.entry("Sell", strategy.short)
    pattern = isShootingStar() ? "Shooting Star" : isDoji() ? "Doji" : isPinBar() ? "Pin Bar" : ""
    label.new(x=bar_index, y=high, text=pattern, color=color.red, textcolor=color.black, size=size.small)

// Stop Loss and Take Profit management for open positions
if (strategy.opentrades > 0)
    if (strategy.position_size > 0)  // Long position
        avg_price_long = strategy.position_avg_price  // Average price of long position
        [long_stop_level, long_take_profit_level] = calculate_levels(strategy.position_size, avg_price_long, stop_loss_pct, take_profit_pct)
        strategy.exit("Exit Long", from_entry="Buy", stop=long_stop_level, limit=long_take_profit_level)
    if (strategy.position_size < 0)  // Short position
        avg_price_short = strategy.position_avg_price  // Average price of short position
        [short_stop_level, short_take_profit_level] = calculate_levels_short(strategy.position_size, avg_price_short, stop_loss_pct, take_profit_pct)
        strategy.exit("Exit Short", from_entry="Sell", stop=short_stop_level, limit=short_take_profit_level)

// Visualization of Support and Resistance Levels
plot(support, title="Support", color=color.green, linewidth=2)
plot(resistance, title="Resistance", color=color.red, linewidth=2)





```

> Detail

https://www.fmz.com/strategy/473937

> Last Modified

2024-12-04 15:19:00
