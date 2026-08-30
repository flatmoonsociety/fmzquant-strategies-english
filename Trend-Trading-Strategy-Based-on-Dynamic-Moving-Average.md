
> Name

Dynamic Moving Average Trading Strategy Trend-Trading-Strategy-Based-on-Dynamic-Moving-Average
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/211fe82e7435facdceb.png)
[trans]

## Overview
This strategy calculates the dynamic moving average and uses it as a trading signal to open a long position when the stock price rises and close the position when the stock price falls. This strategy combines the advantages of momentum indicators and moving averages, aiming to track the mid-term trend of stock prices and achieve stable returns.
## Principle
The strategy is primarily based on three variations of the Hull Moving Average, including the Ordinary Hull Moving Average (HMA), the Weighted Hull Moving Average (WHMA), and the Exponential Hull Moving Average (EHMA). Depending on the code, the policy allows the user to switch between these three Hull MAs.
The calculation formula of HMA is:
HMA = WMA(2*WMA(close,n/2)-WMA(close,n),sqrt(n))

Among them, WMA represents the weighted moving average, and n represents the period parameter. HMA responds to price changes faster than SMA (simple moving average).
The calculation formulas of WHMA and EHMA are similar to HMA. The policy uses HMA as the default option.
After calculating the HMA, this strategy uses the midline value of the HMA as a trading signal. When the price crosses the midline of HMA, enter the long position; when the price crosses the midline of HMA, close the position and exit. In this way, it uses the HMA midline to track the mid-term price trend and achieve profits.
## Advantages
Compared with traditional moving average strategies, this strategy has the following advantages:
1. Faster response, stronger ability to track trends, and timely entry and stop loss
2. Reduce the frequency of unnecessary transactions and avoid chasing ups and downs.
3. Flexible configuration of Hull MA parameters to adapt to a wider market environment
4. Can switch between HMA, WHMA and EHMA to broaden the scope of application
## Risk
There are also some risks with this strategy:
1. It is easy to generate multiple invalid signals during consolidation, thereby increasing transaction frequency and slippage costs.
2. Improper setting of Hull MA parameters may miss the trend reversal point and increase the risk of loss.
3. If you choose stocks improperly and choose stocks with poor liquidity, you may face huge slippages.
Countermeasures:
1. Optimize Hull MA parameters and find the best values
2. Combine with other indicators to determine trend reversal points
3. Select stocks with good liquidity and large average daily trading volume
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Add trading volume or other indicator filters to ensure the reliability of trading signals
2. Combine MACD, KDJ and other indicators to determine the timing of entry and improve the winning rate
3. Adjust Hull MA cycle parameters based on real backtest data
4. Switch to WHMA or EHMA to test which Hull variant performs best on a specific stock
5. Add stop loss strategy to control single loss
## Summarize
This dynamic moving average trading strategy integrates the rapid response advantage of Hull MA, which can effectively track the mid-term trend of stock prices, open long positions and stop loss exits at the right time, and has good historical backtest performance. By further optimizing parameter settings and stock selection range, this strategy can achieve more stable excess returns. It is a quantitative strategy that is easy to implement and has controllable risks.
||

## Overview  

This strategy generates trading signals based on the dynamic moving average to go long when stock prices rise and close positions when prices fall. By combining the advantages of momentum indicators and moving averages, it aims at tracking medium-term price trends for steady profits.  

## Principle

The strategy mainly relies on three Hull Moving Average (HMA) variants – regular HMA, Weighted HMA (WHMA) and Exponential HMA (EHMA). As the code shows, it allows users to switch between the three Hull MAs.  

The formula for HMA is:  

HMA = WMA(2*WMA(close, n/2)-WMA(close, n), sqrt(n))

Where WMA is the Weighted Moving Average and n is the period parameter. Compared to SMA, HMA responds faster to price changes.  

The formulas for WHMA and EHMA are similar. HMA is chosen as the default option.

After calculating the HMA, the strategy uses the midline value of HMA as trading signals. It goes long when the price crosses above the HMA midline and closes positions when the price falls below the line. Thus it tracks medium-term trends using the HMA midline for profits.  

## Advantages

Compared to traditional MA strategies, this strategy has the following edges:  

1. Faster response and stronger trend-following ability for timely entries and stops  
2. Lower unnecessary trade frequency, avoiding chasing surges and stops
3. Flexible HMA parameters for adapting to more market environments   
4. Switchable HMA variants to expand applicability

## Risks

There are also some risks:   

1. Generating multiple false signals during range-bound markets, increasing trade frequency and slippage costs  
2. Missing trend reversal points if HMA parameters are not set properly, leading to greater loss risks
3. Liquidity risk and huge slippage when trading low liquidity stocks  

Solutions:

1. Optimize HMA parameters for best values  
2. Add other indicators to determine trend reversal points  
3. Select liquid stocks with large average daily volume 

## Improvements   

The strategy can also be enhanced from the following aspects:  

1. Add volume or other filters to ensure signal reliability   
2. Combine MACD, KDJ for better timing, improving win rate   
3. Adjust HMA periods based on real-trade backtests  
4. Switch to WHMA or EHMA that performs the best for specific stocks
5. Add stop loss mechanisms to control single trade loss

## Summary  

The dynamic MA trading strategy integrates the fast response of HMA to effectively track medium-term price trends. By opening long positions at appropriate timing and closing stops, it has demonstrated good backtest results. Further improvements in parameter tuning and stock filtering would lead to more steady excess returns. It is an easy-to-implement, risk-controllable quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|Strategy Direction: long|short|all|
|v_input_1|2000|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2030|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|30|Backtest Stop Day|
|v_input_7_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_string_2|0|Hull Variation: Hma|Thma|Ehma|
|v_input_8|55|Length(180-200 for floating S/R , 55 for swing entry)|
|v_input_9|true|Color Hull according to trend?|
|v_input_10|false|Color candles based on Hull's Trend?|
|v_input_11|true|Show as a Band?|
|v_input_12|true|Line Thickness|
|v_input_int_1|40|Band Transparency|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-14 00:00:00
end: 2023-12-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Position Investing by SirSeff', overlay=true, pyramiding=1, default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0)
strat_dir_input = input.string(title='Strategy Direction', defval='long', options=['long', 'short', 'all'])
strat_dir_value = strat_dir_input == 'long' ? strategy.direction.long : strat_dir_input == 'short' ? strategy.direction.short : strategy.direction.all
strategy.risk.allow_entry_in(strat_dir_value)
//////////////////////////////////////////////////////////////////////
// Testing Start dates
testStartYear = input(2000, 'Backtest Start Year')
testStartMonth = input(1, 'Backtest Start Month')
testStartDay = input(1, 'Backtest Start Day')
testPeriodStart = timestamp(testStartYear, testStartMonth, testStartDay, 0, 0)
//Stop date if you want to use a specific range of dates
testStopYear = input(2030, 'Backtest Stop Year')
testStopMonth = input(12, 'Backtest Stop Month')
testStopDay = input(30, 'Backtest Stop Day')
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, 0, 0)


testPeriod() => true
// Component Code Stop
//////////////////////////////////////////////////////////////////////
//INPUT
src = input(close, title='Source')
modeSwitch = input.string('Hma', title='Hull Variation', options=['Hma', 'Thma', 'Ehma'])
length = input(55, title='Length(180-200 for floating S/R , 55 for swing entry)')
switchColor = input(true, 'Color Hull according to trend?')
candleCol = input(false, title='Color candles based on Hull\'s Trend?')
visualSwitch = input(true, title='Show as a Band?')
thicknesSwitch = input(1, title='Line Thickness')
transpSwitch = input.int(40, title='Band Transparency', step=5)

//FUNCTIONS
//HMA
HMA(_src, _length) =>
    ta.wma(2 * ta.wma(_src, _length / 2) - ta.wma(_src, _length), math.round(math.sqrt(_length)))
//EHMA    
EHMA(_src, _length) =>
    ta.ema(2 * ta.ema(_src, _length / 2) - ta.ema(_src, _length), math.round(math.sqrt(_length)))
//THMA    
THMA(_src, _length) =>
    ta.wma(ta.wma(_src, _length / 3) * 3 - ta.wma(_src, _length / 2) - ta.wma(_src, _length), _length)

//SWITCH
Mode(modeSwitch, src, len) =>
    modeSwitch == 'Hma' ? HMA(src, len) : modeSwitch == 'Ehma' ? EHMA(src, len) : modeSwitch == 'Thma' ? THMA(src, len / 2) : na

//OUT
HULL = Mode(modeSwitch, src, length)
MHULL = HULL[0]
SHULL = HULL[2]

//COLOR
hullColor = switchColor ? HULL > HULL[2] ? #00ff00 : #ff0000 : #ff9800

//PLOT
///< Frame
Fi1 = plot(MHULL, title='MHULL', color=hullColor, linewidth=thicknesSwitch, transp=50)
Fi2 = plot(visualSwitch ? SHULL : na, title='SHULL', color=hullColor, linewidth=thicknesSwitch, transp=50)
///< Ending Filler
fill(Fi1, Fi2, title='Band Filler', color=hullColor, transp=transpSwitch)
///BARCOLOR
barcolor(color=candleCol ? switchColor ? hullColor : na : na)


if HULL[0] > HULL[2] and testPeriod()
    strategy.entry('Invest', strategy.long)
if HULL[0] < HULL[2] and testPeriod()
    strategy.entry('Pause', strategy.short)


```

> Detail

https://www.fmz.com/strategy/436100

> Last Modified

2023-12-21 11:33:50
