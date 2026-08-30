
> Name

Multi-Period-Donchian-Channel-Trend-Following-and-Divergence-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d89403471bda06cda6db.png)
![IMG](https://www.fmz.com/upload/asset/2d929efe24f7f21794084.png)


[trans]
#### Overview
This strategy builds a trend following system based on the multi-period Donchian Channel indicator. By analyzing the Tang Qian channel breakthroughs in different time periods and combining the cooperation between the main trend and the local trend, a visually intuitive trend strip pattern is formed. The strategy uses changes in color shades to show the strength of the trend. Green represents an upward trend, and red represents a downward trend. The darker the color, the more obvious the trend.
#### Strategy Principle
The core of the strategy is trend judgment based on the Donchian Channel indicator. Tang Qian channel consists of the highest price channel and the lowest price channel. The trend can be judged by comparing the position relationship between the current price and the channel. It mainly includes the following key components:
1. Judgment of the main trend: Using the 20-period Tang Qian channel, when the price breaks through the upper track, it forms an upward trend, and when it breaks through the lower track, it forms a downward trend.
2. Local trend judgment: Under the main trend framework, use the shorter-period Donchian Channel to judge the direction of the local trend.
3. Trend strip chart: A trend band is formed through a combination of 10 different periods of Donchian channels, and the color depth reflects the strength of the trend.
4. Trading signals: Open long orders when the main trend is upward, open short orders when the main trend is downward, and close positions when the trend reverses.
#### Strategic Advantages
1. Trend judgment is objective: judge the trend based on price breakthroughs to avoid bias caused by subjective judgments
2. Multiple cycle confirmation: improve the accuracy of trend judgment through the superposition of different cycle trends
3. Intuitive visual effect: the color changes of the trend band visually display the market status
4. Clear trading rules: clear entry and exit signals, easy to program
5. Strong adaptability: parameters can be adjusted according to the characteristics of trading varieties to optimize strategy performance
#### Strategy Risk
1. Trend reversal risk: A large retracement may occur at the turning point of the trend.
2. Not applicable to volatile markets: Sideways and volatile markets can easily produce false signals.
3. Parameter sensitivity: Different parameter settings will significantly affect the strategy effect
4. Impact of slippage: Frequent transactions may be affected by slippage
5. Systemic risk: Market emergencies may lead to heavy losses
#### Strategy optimization direction
1. Add trend strength filtering: introduce trend strength indicators such as ADX to filter weak trend signals
2. Optimize stop loss settings: dynamically adjust stop loss positions based on ATR to improve risk control capabilities
3. Add trading volume confirmation: combined with trading volume analysis to verify the validity of the trend
4. Introduce volatility adaptation: dynamically adjust parameters according to market volatility
5. Improve position management: dynamically adjust position size based on trend strength
#### Summary
This strategy builds a trend-following trading system with outstanding visual effects and clear logic through the innovative application of multi-period Donchian channels. The core advantage of the strategy is to visualize the complex trend analysis process, making it easier for traders to intuitively grasp market trends. Through reasonable parameter optimization and risk control measures, this strategy has good practical application value. It is recommended that traders pay attention to the choice of market environment when applying real offers, and conduct position management based on their own risk tolerance.
|| 

#### Overview
This strategy builds a trend following system based on multi-period Donchian Channels. By analyzing Donchian Channel breakouts across different timeframes and combining main and local trend relationships, it forms an visually intuitive trend ribbon. The strategy uses varying color depths to display trend strength, with green representing uptrends and red representing downtrends, where deeper colors indicate more pronounced trends.

#### Strategy Principles
The core of the strategy is trend determination based on the Donchian Channel indicator. The Donchian Channel consists of upper and lower bands, determining trends by comparing current price position relative to the channel. Key components include:
1. Main trend determination: Using 20-period Donchian Channel, uptrend forms when price breaks above upper band, downtrend forms when breaking below lower band
2. Local trend determination: Under the main trend framework, shorter period Donchian Channels determine local trend direction
3. Trend ribbon: Combination of 10 different period Donchian Channels forms a trend ribbon, with color depth reflecting trend strength
4. Trading signals: Long entries on uptrend, short entries on downtrend, positions closed on trend reversal

#### Strategy Advantages
1. Objective trend determination: Based on price breakouts, avoiding subjective judgment bias
2. Multi-period confirmation: Improves trend determination accuracy through multiple timeframe trend overlay
3. Intuitive visualization: Trend ribbon color changes clearly display market conditions
4. Clear trading rules: Entry and exit signals are well-defined for programmatic implementation
5. High adaptability: Parameters can be adjusted to optimize strategy performance for different instruments

#### Strategy Risks
1. Trend reversal risk: Significant drawdowns possible at trend turning points
2. Unsuitable for ranging markets: False signals likely during sideways consolidation
3. Parameter sensitivity: Different parameter settings significantly affect strategy performance
4. Slippage impact: Frequent trading may be affected by slippage
5. Systematic risk: Market events may cause major losses

#### Strategy Optimization Directions
1. Add trend strength filtering: Incorporate ADX and other trend strength indicators to filter weak trend signals
2. Optimize stop loss settings: Dynamically adjust stop loss positions based on ATR for better risk control
3. Add volume confirmation: Incorporate volume analysis to verify trend validity
4. Introduce volatility adaptation: Dynamically adjust parameters based on market volatility
5. Improve position management: Dynamically adjust position size based on trend strength

#### Summary
This strategy creates a visually striking and logically clear trend following trading system through innovative application of multi-period Donchian Channels. The core advantage lies in visualizing complex trend analysis processes, making it easier for traders to intuitively grasp market trends. Through proper parameter optimization and risk control measures, this strategy has good practical application value. Traders are advised to consider market conditions carefully when implementing live trading and manage positions according to their risk tolerance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-12 00:00:00
end: 2025-02-19 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Donchian Trend Ribbon Strategy", shorttitle="DonchianTrendRibbonStrat", overlay=true, precision=0)

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Parameters
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
dlen = input.int(defval=20, title="Donchian Channel Period", minval=10)

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Helper function to determine color
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
f_color(mainTrend, localTrend) =>
    // mainTrend = 1 => uptrend, -1 => downtrend
    // localTrend = 1 => local uptrend, -1 => local downtrend
    // Return color based on whether local trend aligns with the main trend
    color c = na
    if mainTrend == 1
        c := localTrend == 1 ? color.new(color.lime, 0) : color.new(color.lime, 60)
    else if mainTrend == -1
        c := localTrend == -1 ? color.new(color.red, 0) : color.new(color.red, 60)
    else
        c := na
    c

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Function dchannel - determines main trend (1 or -1)
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
dchannel(len) =>
    float hh = ta.highest(len)
    float ll = ta.lowest(len)
    var int tr = 0
    tr := close > hh[1] ? 1 : close < ll[1] ? -1 : nz(tr[1])

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Function dchannelalt - determines local trend and returns color
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
dchannelalt(len, maintrend) =>
    float hh = ta.highest(len)
    float ll = ta.lowest(len)
    var int tr = 0
    tr := close > hh[1] ? 1 : close < ll[1] ? -1 : nz(tr[1])
    f_color(maintrend, tr)

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Calculate main trend
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
maintrend = dchannel(dlen)

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Plotting the Donchian Trend Ribbon
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
plot( 5,  color=dchannelalt(dlen - 0, maintrend),  style=plot.style_columns, histbase= 0)
plot(10, color=dchannelalt(dlen - 1, maintrend),   style=plot.style_columns, histbase= 5)
plot(15, color=dchannelalt(dlen - 2, maintrend),   style=plot.style_columns, histbase=10)
plot(20, color=dchannelalt(dlen - 3, maintrend),   style=plot.style_columns, histbase=15)
plot(25, color=dchannelalt(dlen - 4, maintrend),   style=plot.style_columns, histbase=20)
plot(30, color=dchannelalt(dlen - 5, maintrend),   style=plot.style_columns, histbase=25)
plot(35, color=dchannelalt(dlen - 6, maintrend),   style=plot.style_columns, histbase=30)
plot(40, color=dchannelalt(dlen - 7, maintrend),   style=plot.style_columns, histbase=35)
plot(45, color=dchannelalt(dlen - 8, maintrend),   style=plot.style_columns, histbase=40)
plot(50, color=dchannelalt(dlen - 9, maintrend),   style=plot.style_columns, histbase=45)

//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
// Trading Logic (STRATEGY)
//~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
bool goLong  = (maintrend == 1)
bool goShort = (maintrend == -1)

// Entry signals
if goLong
    strategy.entry("Long", strategy.long)

if goShort
    strategy.entry("Short", strategy.short)

// Close positions when trend changes
if strategy.position_size > 0 and goShort
    strategy.close("Long")

if strategy.position_size < 0 and goLong
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/483040

> Last Modified

2025-02-21 10:38:06
