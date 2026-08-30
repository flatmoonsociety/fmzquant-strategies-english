
> Name

Gandalf quantitative trading strategy Gandalf-Mean-Reversion-Quantitative-Trading-Strategy based on the median line
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11996521f6f353fc85b.png)

[trans]

### Overview
The Gandalf quantitative trading strategy is a trend following strategy based on the median line. It determines the current trend direction by calculating the weighted average price, median line and entity middle price to find a better entry point. When a trend reversal is detected, it will quickly stop the loss and exit. This strategy combines the strategic ideas of trend following and trend reversal.
### Strategy Principles
The core logic of the Gandalf strategy is to compare the size relationship between the weighted average price, the median line and the entity's middle price to determine the direction and strength of the current trend.
Specifically, it calculates the following prices:
- Weighted average price: (highest price + lowest price + closing price + closing price) / 4
- Median line: (highest price + lowest price) / 2
- Entity middle price: (opening price + closing price) / 2
When entering the market, it will compare the size relationship between the weighted average price of the first two K lines, the median line and the middle price of the entity to determine whether it meets the characteristics of trend start.
For example, if the weighted average price is lower than the median line, and the middle price of the entity is also lower than the weighted average price, it means that the price is falling, and this is a shorting opportunity.
When exiting the stop loss, it will continue to compare the size relationship between these prices to determine whether there are signs of a trend reversal. If the weighted average price is higher than the middle price of the entity, and the median line is also lower than the weighted average price, it means that the trend has reversed, and the loss should be stopped immediately.
Through this method of comparing price relationships, the Gandalf strategy realizes the judgment and tracking of trends. It can not only find better entry opportunities, but also quickly detect trend reversals and stop losses.
### Strategic Advantages
The Gandalf strategy has the following advantages:
1. Using the median line to determine the trend direction can effectively filter out market noise and lock in the main trend.
2. Entry conditions combined with multiple price comparisons can more reliably determine the start of a trend.
3. Stop loss conditions also use price comparison to determine trend reversal, which can quickly stop losses and control risks.
4. By placing conditional orders, you can enter the market near the ideal price.
5. The number of take-profits and position limit can be set in advance to lock in profits and control the risk of a single transaction.
6. The code structure is clear and simple, easy to understand and modify.
7. Parameters can be adjusted according to personal risk preferences and are easy to optimize.
8. Suitable for trending varieties, you can obtain trends and make profits.
In general, the Gandalf strategy uses the median line to determine the trend and sets take-profit and stop-loss conditions, which can effectively control risks and track the trend. It is a reliable trend following strategy.
### Strategy Risk
The Gandalf strategy also has certain risks that need to be noted:
1. As a trend following strategy, more small losses will occur when the trend is not obvious or reversals are frequent.
2. Failure to effectively judge the trend reversal point may lead to expanded losses.
3. In the consolidation market, it is easy to be arbitraged.
4. Depends on parameter settings, parameters need to be adjusted for different varieties.
5. If you hold a unilateral position, you cannot make profits by taking advantage of the reverse market trend.
6. The failure rate of conditional orders is high, and you may have to wait for a long time to enter the market.
Corresponding risk management measures:
1. Use small positions and enter the market in batches to control single losses.
2. Set a stop loss line and stop the loss quickly. Or use a trailing stop to trail the stop.
3. Optimize parameters and adjust them to suit the current variety. It can assist in judging trends with other indicators.
4. Martingale replenishment method can be used to reduce costs.
5. Trade varieties with obvious trends and have high profit confidence.
6. Relax entry conditions appropriately and take into account the probability of entry.
### Strategy optimization direction
The Gandalf strategy can also be optimized from the following aspects:
1. Construct trend judgment indicators to assist in judging the timing of trend reversal. For example, add MACD, Bollinger Bands and other judgments.
2. Add discrete optimization function to automatically optimize parameters and adapt to more varieties.
3. Add machine learning algorithms and use historical data to train neural networks or SVM models to determine trends.
4. Added take-profit methods, such as moving take-profit and index moving take-profit.
5. Combine with related products to conduct price difference arbitrage or statistical arbitrage.
6. Add state prediction based on hidden Markov model to determine the market state.
7. Construct composite strategies, such as combining with moving average strategies, to achieve multi-strategy management.
8. Explore the optimization of trading strategy combinations and find the combination weight.
Generally speaking, the Gandalf strategy can be expanded and optimized at multiple levels such as trend judgment, automatic optimization, and risk management, making the strategy more stable and reliable.
### Summarize
The Gandalf quantitative strategy is a simple and effective strategy for judging trends based on price comparisons. It combines the ideas of trend tracking and quick stop loss to effectively control risks. The logic of this strategy is clear and easy to understand, and parameters can be adjusted according to personal risk preferences. However, it also has certain profit fluctuations and position risks, which require appropriate optimization and management. Overall, the Gandalf strategy is a reliable, easy-to-master and optimized trend following strategy, suitable for pursuing stable trend profits.
||

### Overview

The Gandalf quantitative trading strategy is a mean reversion strategy based on median price lines. It determines the current trend direction by calculating weighted average price, median price line and body middle price, to find optimal entry points. When a trend reversal is detected, it will quickly cut losses and exit. The strategy combines the ideas of trend following and trend reversal strategies.

### Strategy Logic

The core logic of Gandalf strategy is to compare the magnitude relationship between weighted average price, median price line and body middle price, to judge the current trend direction and strength. 

Specifically, it calculates the following prices:

- Weighted average price: (Highest price + Lowest price + Close price + Close price) / 4
- Median price line: (Highest price + Lowest price) / 2  
- Body middle price: (Open price + Close price) / 2

When entering a position, it compares the magnitude relationship between the weighted average price, median price line and body middle price of the last two bars, to determine whether it fits the characteristics of a starting trend.

For example, if the weighted average price is below the median price line, and the body middle price is also below the weighted average price, it indicates the price is falling, which presents a shorting opportunity.

When stopping loss, it continues to compare the magnitude relationship between these prices, to judge whether there are signs of trend reversal. If the weighted average price is above the body middle price, and the median price line is below the weighted average price, it indicates a trend reversal, and should cut loss immediately.

By comparing the price magnitude relationship, Gandalf strategy realizes the judgment and tracking of trends. It can find optimal entry timing, and also quickly detect trend reversals to stop loss.

### Advantages

The Gandalf strategy has the following advantages:

1. Using median price line to determine trend direction can effectively filter market noise and lock in the major trend.

2. The entry condition combining multiple price comparisons can more reliably determine the start of a trend.

3. The stop loss condition also uses price comparison to judge trend reversal, which allows fast stop loss and risk control.

4. Adopting conditional orders for entry can get in at ideal prices. 

5. Preset maximum profit take times and holding period upper limit can lock in profits and control single trade risks.

6. The code structure is clear and simple, easy to understand and modify.

7. Parameters can be adjusted based on personal risk preference, easy to optimize.

8. Applicable to trending products, able to capture trending profits.

In summary, the Gandalf strategy utilizes median line to determine trend, sets profit taking and stop loss conditions, and can effectively control risks while tracking trends, making it a reliable trend following strategy.

### Risks

The Gandalf strategy also has some risks to note:

1. As a trend following strategy, it will produce more small losses when trend is unclear or frequently reversing.

2. Unable to effectively determine trend reversal points, may lead to expanding losses.

3. Prone to being trapped in range-bound markets.

4. Relies on parameter settings, parameters need adjusting for different products.

5. Unidirectional holding, unable to profit from reverse trends. 

6. High failure rate of conditional orders, may wait long for entry.

Risk management measures:

1. Adopt small position sizing, partial entry, to control single loss.

2. Set stop loss line, fast stop loss. Or adopt moving stop loss or trailing stop loss.

3. Optimize parameters to suit current product. Use other indicators to assist trend judgment.

4. Consider martingale to lower cost basis.

5. Trade products with obvious trends, higher profit confidence. 

6. Relax entry criteria appropriately to improve entry probability.

### Improvement Directions

The Gandalf strategy can also be improved in the following aspects:

1. Build trend judgment indicators to assist in determining timing of trend reversals, such as adding MACD, Bollinger Bands etc.

2. Add discrete optimization functions to auto optimize parameters and adapt to more products.

3. Increase machine learning algorithms, train neural networks or SVM models on historical data to judge trends.

4. Add more profit taking methods, like moving profit take, parabolic profit take.

5. Combine related products for spread trading or stat arb strategies. 

6. Add state prediction based on Hidden Markov Model to judge market regime.

7. Construct combined strategies, like combining with moving average strategies for multi-strategy management.

8. Explore optimization of trading strategy combinations to find optimal portfolio weights.

In summary, the Gandalf strategy can be expanded and optimized in multiple dimensions like trend judgment, automatic optimization, risk management, to make the strategy more robust and reliable.

### Conclusion

The Gandalf quantitative strategy is a simple yet effective strategy based on price comparison to determine trends. It combines the ideas of trend following and quick stop loss, and can effectively control risks. The strategy logic is clear and easy to understand, parameters can be adjusted based on personal risk preferences. But it also has some profit fluctuation and holding risks, requiring proper optimization and management. Overall, the Gandalf strategy is a reliable, easy to grasp and optimize trend following strategy, suitable for pursuing steady trend profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Quantity (0 to auto calc)|
|v_input_2|10000|Money to spend on single trade|
|v_input_3|6|Max Profit Close|
|v_input_4|8|Max Total Bars|
|v_input_5|-0.08|Distance from low price to place entry limit|
|v_input_6|true|Use Alt Exit|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-22 00:00:00
end: 2023-10-29 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3

// The GandalfProjectResearchSystem strategy, as discussed in
// “System Development Using Artificial Intelligence”
// by Domenico D’Errico and Giovanni Trombetta
strategy("Gandalf Project Research System", overlay=true)

// Inputs
Quantity = input(0, title="Quantity (0 to auto calc)")
Single_Trade_Money = input(10000, minval=1, title="Money to spend on single trade")
MaxProfitCloses = input(6, minval=1, title="Max Profit Close")
MaxBars = input(8, minval=1, title="Max Total Bars")
Enter_Gap = input(-0.08, title="Distance from low price to place entry limit")
AltExit = input(true, title="Use Alt Exit")

// Calculate Order Quantity
Ncon = Single_Trade_Money / close

// Misc Variables
src = close
BarsSinceEntry = 0
MaxProfitCount = 0
MedBodyPrice = (open + close) / 2.0
Weighted = (high + low + close + close) / 4.0
Median = (high + low) / 2.0

// Enter Conditions
Cond00 = strategy.position_size == 0
Cond01 = ((Weighted[1] < Median[1] and Median[2] <= Weighted[1] and MedBodyPrice[2] <= Weighted[3]) or (Weighted[1] < Median[3] and MedBodyPrice[0] < Median[2] and MedBodyPrice[1] < MedBodyPrice[2]))
Entry01 = Cond00 and Cond01

// Update Exit Variables
BarsSinceEntry := Cond00 ? 0 : nz(BarsSinceEntry[1]) + 1
MaxProfitCount := Cond00 ? 0 : (close > strategy.position_avg_price and BarsSinceEntry > 1) ? nz(MaxProfitCount[1]) + 1 : nz(MaxProfitCount[1])

// Exit Conditions
eCond01 = BarsSinceEntry - 1 >= MaxBars
eCond02 = MaxProfitCount >= MaxProfitCloses
eCond03 = ((Weighted[1] < MedBodyPrice[1] and Median[2] == MedBodyPrice[3] and MedBodyPrice[1] <= MedBodyPrice[4]) or (Weighted[2] < MedBodyPrice[0] and Median[4] <= Weighted[3] and MedBodyPrice[1] <= Weighted[1]) or (Weighted[2] < MedBodyPrice[0] and Median[4] <= Weighted[3] and MedBodyPrice[1] <= Weighted[1]))
eCond04 = AltExit ? true : close - strategy.position_avg_price < 0
Exit01 = not Cond00 and (eCond01 or eCond02 or (eCond03 and eCond04))

// Entries
strategy.entry(id="L1", long=true, limit=low + Enter_Gap, qty=(Quantity > 0 ? Quantity : Ncon), when=Entry01)
 
// Exits
strategy.close("L1", Exit01)

```

> Detail

https://www.fmz.com/strategy/430542

> Last Modified

2023-10-30 10:33:17
