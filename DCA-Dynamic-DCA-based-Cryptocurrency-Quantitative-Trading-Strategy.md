
> Name

Dynamic-DCA-based-Cryptocurrency-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d87668986448175d4858.png)
![IMG](https://www.fmz.com/upload/asset/2d90fdc309b085a7c667d.png)


[trans]
#### Overview
This is a quantitative trading strategy specially designed for the cryptocurrency market. It makes full use of the high volatility characteristics of the cryptocurrency market and dynamically adds positions when prices fall back through intelligent cost averaging (DCA). The strategy operates on a 15-minute time frame and is able to effectively respond to the rapid fluctuations in the cryptocurrency market while avoiding the risks of over-trading.
#### Strategy Principle
The strategy mainly consists of four core modules:
1. Intelligent entry system: Based on the OHLC4 weighted average price, the first position is opened to adapt to the high volatility characteristics of the cryptocurrency market.
2. Dynamic position covering mechanism: safety orders are triggered when prices fall back, and the amount of position covering increases with depth, taking full advantage of market fluctuations.
3. Risk management system: Optimize the risk-return ratio through pyramidal position addition and flexible leverage adjustment
4. Quick profit-taking control: a profit-taking mechanism designed for the rapid fluctuations of the cryptocurrency market, including handling fee optimization
#### Strategic Advantages
1. Market adaptability: specifically optimized for the high volatility characteristics of the cryptocurrency market
2. Risk diversification: reduce sudden risks in the cryptocurrency market through dynamic batch opening of positions
3. Arbitrage efficiency: Make full use of price fluctuations in the cryptocurrency market to obtain profits
4. Automated execution: supports API access to multiple mainstream cryptocurrency exchanges
5. Fund efficiency: Improve the fund utilization efficiency of cryptocurrency trading through intelligent leverage management
#### Strategy Risk
1. Market risk: Extreme fluctuations in the cryptocurrency market may lead to larger drawdowns
2. Liquidity risk: Some small-cap cryptocurrencies may face illiquidity issues
3. Leverage risk: The high volatility of the cryptocurrency market increases the risk of leveraged trading
4. Technical risk: Relying on the stability of the exchange API and the quality of the network connection
5. Regulatory risks: Policy changes in the cryptocurrency market may affect strategy execution
#### Strategy optimization direction
1. Volatility Adaptation: Introducing volatility indicators unique to the cryptocurrency market to dynamically adjust parameters
2. Multi-currency collaboration: Develop multi-currency linked transaction logic to diversify single currency risks
3. Market sentiment filtering: Integrate cryptocurrency market sentiment indicators to optimize entry timing
4. Transaction cost optimization: reduce costs through intelligent routing and exchange selection
5. Risk early warning mechanism: Establish an early warning system based on abnormal market fluctuations
#### Summary
This strategy provides a comprehensive automated solution for cryptocurrency trading through innovative DCA methods and dynamic risk management. Although the cryptocurrency market has higher risks, through carefully designed risk control mechanisms and market adaptability optimization, the strategy can maintain stability in most market environments. Future optimization will focus on improving the strategy’s adaptability to the particularities of the cryptocurrency market. ||
#### Overview
This is a quantitative trading strategy specifically designed for the cryptocurrency market, leveraging its high volatility characteristics through intelligent Dollar-Cost Averaging (DCA) with dynamic position scaling during price retracements. Operating on a 15-minute timeframe, it effectively handles rapid cryptocurrency market fluctuations while avoiding overtrading risks.

#### Strategy Principles
The strategy consists of four core modules:
1. Smart Entry System: Initial position based on OHLC4 weighted average price, adapted to cryptocurrency market volatility
2. Dynamic Accumulation Mechanism: Triggers safety orders during price retracements, scaling position size with depth to utilize market volatility
3. Risk Management System: Optimizes risk-reward ratio through pyramiding and flexible leverage adjustment
4. Rapid Take-Profit Control: Designed for cryptocurrency market's quick fluctuations, including fee optimization

#### Strategy Advantages
1. Market Adaptability: Specifically optimized for cryptocurrency market's high volatility
2. Risk Diversification: Reduces sudden risks in cryptocurrency markets through dynamic staged positioning
3. Arbitrage Efficiency: Effectively captures profits from cryptocurrency price volatility
4. Automated Execution: Supports API integration with major cryptocurrency exchanges
5. Capital Efficiency: Improves capital utilization through intelligent leverage management

#### Strategy Risks
1. Market Risk: Extreme cryptocurrency volatility may lead to significant drawdowns
2. Liquidity Risk: Some small-cap cryptocurrencies may face insufficient liquidity
3. Leverage Risk: High cryptocurrency volatility increases leverage trading risks
4. Technical Risk: Depends on exchange API stability and network connection quality
5. Regulatory Risk: Cryptocurrency market policy changes may affect strategy execution

#### Strategy Optimization Directions
1. Volatility Adaptation: Introduce cryptocurrency-specific volatility indicators for dynamic parameter adjustment
2. Multi-coin Synergy: Develop multi-cryptocurrency trading logic to diversify single-coin risk
3. Market Sentiment Filtering: Integrate cryptocurrency market sentiment indicators to optimize entry timing
4. Transaction Cost Optimization: Reduce costs through smart routing and exchange selection
5. Risk Alert Mechanism: Establish warning system based on market abnormal fluctuations

#### Summary
The strategy provides a comprehensive automated solution for cryptocurrency trading through innovative DCA methods and dynamic risk management. While cryptocurrency markets carry high risks, the strategy maintains stability in most market conditions through carefully designed risk control mechanisms and market adaptability optimization. Future improvements will focus on enhancing strategy adaptation to cryptocurrency market specificities.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2020-08-29 15:00:00
end: 2025-02-18 17:22:45
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"TRB_USDT"}]
*/

//@version=5
strategy('Autotrade.it DCA', overlay=true, pyramiding=999, default_qty_type=strategy.cash, initial_capital=10000, commission_value=0.02)

// Date Ranges
from_month = 1
from_day = 1
from_year = 2021
to_month = 1
to_day = 1
to_year = 9999
start = timestamp(from_year, from_month, from_day, 00, 00)  // backtest start window
finish = timestamp(to_year, to_month, to_day, 23, 59)  // backtest finish window
window = time >= start and time <= finish ? true : false  // create function "within window of time"

source_type = 'OHLC4'
source_function(type) =>
    if type == 'Close'
        close
    else if type == 'Open'
        open
    else if type == 'High'
        high
    else if type == 'Low'
        low
    else if type == 'HL2'
        hl2
    else if type == 'HL3'
        hlc3
    else if type == 'OHLC4'
        ohlc4
    else if type == 'Median Body'
        (open + close) / 2
    else if type == 'Weighted Close'
        (high + low + 2 * close) / 4
    else if type == 'Trend Biased'
        close > open ? (high + close) / 2 : (low + close) / 2
    else if type == 'Trend Biased Extreme'
        close > open ? high : low
truncate(number, decimals) =>
    factor = math.pow(10, decimals)
    int(number * factor) / factor
// Strategy Inputs
price_deviation = input.float(1.0, title='Price deviation to open safety orders (%)', minval=0.0) / 100
take_profit = 1.0 / 100
base_order = 10.0
safe_order = 10.0
safe_order_volume_scale = 1.1
safe_order_step_scale = 1.1
max_safe_order = 30

var current_so = 0
var initial_order = 0.0
var previous_high_value = 0.0
var original_ttp_value = 0.0
// Calculate our key levels
take_profit_level = strategy.position_avg_price * (1 + take_profit)
startTrade = input.int(defval=1, title='Trade Start')
margin = input.float(title='Margin', defval=1, step=1, tooltip='USDT')
leverage = input.int(title='Leverage', defval=50, tooltip='it only used on futures trade')
multi = 1.125
var float multiplier = 1
symbol = str.replace_all(syminfo.ticker, '.P', '')
var float totalMargin = 0.0
var bool isTrade =false
var float totalPrice = 0.0
var int totalTrade = 0
var float totalQtys = 0
var float sellPrice = 0
var float sellQty = 0


// // First Position
if strategy.position_size == 0 and window and source_function(source_type) > 0 and previous_high_value == 0.0
    strategy.entry('No Position', strategy.long, qty=base_order / source_function(source_type))
    initial_order := source_function(source_type)
    current_so := 1
    previous_high_value := 0.0
    original_ttp_value := 0
    original_ttp_value

threshold = 0.0
if safe_order_step_scale == 1.0
    threshold := initial_order - initial_order * price_deviation * safe_order_step_scale * current_so
    threshold
else
    threshold := initial_order - initial_order * ((price_deviation * math.pow(safe_order_step_scale, current_so) - price_deviation) / (safe_order_step_scale - 1))
    threshold

// Average Down
if current_so > 0 and source_function(source_type) <= threshold and current_so <= max_safe_order and previous_high_value == 0.0
    if(startTrade<=current_so)
        margin := math.round(margin * multiplier * 100) / 100
        multiplier *= multi
        totalMargin += margin
        avePrice = (totalPrice/totalTrade)
        qty = margin*leverage/close
        isTrade := true
        totalPrice+=close
        totalTrade+=1
        totalQtys+=qty
        alert('{"category": "linear", "mode": 3, "tradeMode": 0, "symbol": "' + str.tostring(symbol) + '", "leverage": "' + str.tostring(leverage) + '", "side": "Buy", "orderType": "Market", "marketUnit": "quoteCoin", "qty": "' + str.tostring(margin) + '", "reduceOnly": false, "positionIdx": 1 }')
        strategy.entry('Trade # ' + str.tostring(current_so) +"---Margin: $" + str.tostring(margin), direction=strategy.long, qty=safe_order * math.pow(safe_order_volume_scale, current_so - 1) / source_function(source_type))
    else
        strategy.entry('Trade # ' + str.tostring(current_so) +" No position", direction=strategy.long, qty=safe_order * math.pow(safe_order_volume_scale, current_so - 1) / source_function(source_type))
    current_so += 1
    current_so


// Take Profit!
if take_profit_level <= source_function(source_type) and strategy.position_size > 0 or previous_high_value > 0.0
    if(isTrade)
        avePrice = totalMargin * leverage / totalQtys * 1.002  // Include fee directly
        percentGain = math.round((close - avePrice) / avePrice * 100 * 100) / 100
        gain = math.round(percentGain * leverage * totalMargin / 100 * 100) / 100
        isTrade := false
        sellPrice := avePrice*0.95
        sellQty := totalMargin * leverage/sellPrice
        loop = current_so-1
        testQty = sellQty/loop
        strategy.close_all(comment= "Take Profit: $" + str.tostring(gain))
        alert('{"category": "linear", "mode": 3, "tradeMode": 0, "symbol": "' + str.tostring(symbol) + '", "leverage": "' + str.tostring(testQty) + '", "side": "Sell", "orderType": "Market", "marketUnit": "baseCoin", "qty": "' + str.tostring(sellQty) + '", "reduceOnly": true, "positionIdx": 1, "loop": "' + str.tostring(loop) + '" }')
                    
    else
        strategy.close_all(comment='No Position')
    current_so := 0
    previous_high_value := 0
    original_ttp_value := 0
    multiplier:=1
    totalMargin:=0.0
    totalPrice:=0
    totalTrade:=0
    totalQtys:=0


```

> Detail

https://www.fmz.com/strategy/482672

> Last Modified

2025-02-27 17:56:06
