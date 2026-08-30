
> Name

Trading strategy based on RSI mean reversion RSI-Average-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy uses multiple price inputs to calculate the average RSI and determine whether the price is overbought and oversold. It is a reversal trading strategy.
## Strategy Principle
1. Calculate the RSI value based on the closing price, opening price, highest price, etc.
2. Take the arithmetic average of multiple RSI values ​​to obtain the RSI mean.
3. An RSI average above 0.5 is an overbought signal, and below 0.5 is an oversold signal.
4. A reversal trading signal is generated when the RSI average returns to the 0.5 midline.
5. Set the RSI average exit threshold. If it breaks through the 0.65 area, close the long position, and if it breaks through the 0.35 area, close the short position.
6. The transaction logic is simple, clear and easy to implement.
## Advantage Analysis
1. Use a variety of price information to calculate the RSI average to improve stability.
2. The RSI mean returns to the center line to generate trading signals, which have both trend and reversal characteristics.
3. The intuitive RSI mean curve forms a clear visual trading signal.
4. The default parameters are simple and practical, suitable for reversal traders.
5. The code is concise, easy to understand and modify, and is suitable for beginners with technical skills.

## Risk Analysis
1. The RSI indicator can easily form false reversal signals, leading to losses.
2. Improper setting of RSI parameters and midline threshold will affect the strategy performance.
3. Based only on a single RSI indicator, the systemic risk is relatively high.
4. Unable to determine price reversal sustaining ability.
5. It is easy to cause losses under trending market conditions.

## Optimization direction
1. Test and optimize RSI cycle parameters to improve indicator sensitivity.
2. Evaluate the impact of different price inputs on the RSI mean.
3. Add a trend filter to avoid counter-trend trading.
4. Combine with other factors to confirm reversal signals.
5. Establish a dynamic stop-loss mechanism to control risks.
6. Optimize entry, stop loss, and take profit strategies to improve strategy efficiency.
## Summarize
This strategy uses RSI mean reversal trading, which is simple and easy to implement and suitable for beginners. However, there are risks of signal misjudgment and trend. Through multi-factor optimization and risk management improvements, the strategy can be made more robust and efficient and become a reliable reversal trading system.
||

## Overview 

This strategy uses RSI average based on multiple price inputs to determine overbought/oversold and trades mean-reversion.

## Strategy Logic

1. Calculate RSI values based on close, open, high etc. 

2. Take arithmetic average of the RSI values to derive RSI mean.

3. RSI mean above 0.5 indicates overbought, below 0.5 oversold.

4. RSI mean reversion to the 0.5 midpoint generates trading signals.

5. Set RSI mean exit thresholds, like close long above 0.65, close short below 0.35.

6. Simple and clear trading logic easy to implement.

## Advantages

1. RSI mean improves stability using multiple price inputs.

2. Trading signals from RSI mean reversion, combining trend and reversal.

3. Intuitive RSI mean curve forms clear visual trading signals.

4. Default parameters simple and practical for mean reversion.

5. Concise code easy to understand and modify for beginners.


## Risks

1. RSI prone to false reversal signals resulting in losses. 

2. Inappropriate RSI parameters and threshold setups affect performance.

3. Relying solely on single RSI indicator leads to higher systematic risk.

4. Unable to confirm price reversal sustaining power. 

5. Trending markets tend to produce losses.


## Enhancement

1. Test and optimize RSI period for higher sensitivity.

2. Evaluate price input impacts on RSI mean.

3. Add trend filter to avoid counter-trend trades.

4. Incorporate other factors to confirm reversal signals.

5. Build dynamic stops mechanism for risk control.

6. Optimize entry, stop loss, take profit for higher efficiency.

## Conclusion

This strategy trades RSI mean reversion simply and viably for beginners. But risks include signal errors and trends exist. Multi-factor optimization and risk management improvements can make the strategy more robust and efficient as a reliable reversal system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|0.65|v_input_float_1|
|v_input_float_2|0.35|v_input_float_2|
|v_input_bool_1|true|(?Entries Type)Allow Long entries|
|v_input_bool_2|true|Allow Short entries|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-13 00:00:00
end: 2023-09-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=5
strategy("RSI Average Swing Bot")

long_only=input.bool(true, title="Allow Long entries", group="Entries Type")
short_only=input.bool(true, title="Allow Short entries", group="Entries Type")
rsiohlc4= ta.rsi(ohlc4,50)/100
rsiclose= ta.rsi(close,50)/100
rsiopen= ta.rsi(open,50)/100
rsihigh= ta.rsi(high,50)/100
rsihlc3= ta.rsi(hlc3,50)/100
rsihl2= ta.rsi(hl2,50)/100

hline(0.3, color=color.white, linestyle=hline.style_dashed, linewidth=2)
hline(0.5, color=color.white, linestyle=hline.style_dotted, linewidth=2)
hline(0.7, color=color.white, linestyle=hline.style_dashed, linewidth=2)
rsi_avg = (rsiohlc4+rsiclose+rsiopen+rsihigh+rsihl2+rsihlc3)/6

culoare = rsi_avg > 0.50? color.green : rsi_avg<0.50 ? color.red : color.yellow
plot(rsi_avg,color=culoare )


long = rsi_avg > 0.5 and rsi_avg[1]< 0.5
longexit = rsi_avg >= input.float(0.65, step=0.05)
short = rsi_avg < 0.5 and rsi_avg[1] >0.5
shortexit=rsi_avg<=input.float(0.35, step=0.05)

if(long_only)
    strategy.entry("long",strategy.long,when=long)
    strategy.close("long",when=longexit or short)

if(short_only)
    strategy.entry("short",strategy.short,when=short)
    strategy.close("short",when=shortexit or long)




```

> Detail

https://www.fmz.com/strategy/427384

> Last Modified

2023-09-20 15:38:45
