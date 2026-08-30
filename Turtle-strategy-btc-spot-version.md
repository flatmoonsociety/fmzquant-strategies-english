
> Name

Turtle strategy btc spot version
> Author

groot

> Strategy Description

Seeing that there is no public python turtle strategy on the platform, I wrote a simple one myself.
The Turtle system, which is close to the original version, has not been optimized very much. It can be used as a backtest test. You can also optimize it yourself and run it in real time.
Open a position: Open a position after surpassing Tang Qian on track
Add a position: Add a position if it exceeds 0.5ATR of the previous price
Stop loss and take profit: if it falls below the lower track or falls below the last opening price - 2ATR, all profits will be taken.
One year of data was backtested, with an annualized rate of 80% and a maximum drawdown of 16%.
The utilization rate of spot funds is low, and the income will be higher after changing to the contract version.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|fresh_rete|24|Transaction frequency (hours)|
|trade_percent|0.01|Asset ratio|
|DC_range|30|Number of channel cycles|
|atrlength|24|atr cycle number|

> Source (python)

``` python
'''backtest
start: 2019-01-01 00:00:00
end: 2020-03-02 00:00:00
period: 1d
exchanges: [{"eid":"OKEX","currency":"BTC_USDT","stocks":0}]
args: [["fresh_rete",24],["DC_range",20],["atrlength",14]]
'''


import numpy as np
import pandas as pd
import datetime


data = {'ordertime':[],'id':[],'price':[]}
hisorder = pd.DataFrame(data)
    
def turtle():
    #声明全局变量
    global hisorder
    
    acct = exchange.GetAccount()

    records=exchange.GetRecords(fresh_rete*60*60)

    ticker = exchange.GetTicker()
    

    portfolio_value = acct.Balance+acct.FrozenBalance+(acct.Stocks+acct.FrozenStocks)*records[-1]['Close']
    atr = TA.ATR(records, atrlength)[-1]
    #计算得到unit大小
    value = portfolio_value*trade_percent
    unit =  min(round(value/atr,4),round(acct.Balance/(ticker['Last']+100),4))
    #unit =  round(value/atr,2)

    df = pd.DataFrame(records)
    current_price = records[-1]['Close']
    last_price = 0
    if len(hisorder)!=0:
        last_price = hisorder.iloc[-1]['price']
    max_price = df[-DC_range:-2]['High'].max()
    min_price = df[-int(DC_range/2):-2]['Low'].min() 
    
    opensign = len(hisorder)==0 and current_price > max_price
    

    addsign = len(hisorder)!=0 and current_price > last_price + 0.5*atr


    stopsign = len(hisorder)!=0 and current_price < min_price
    
    
    closesign = len(hisorder)!=0 and current_price < (last_price - 2*atr)

    
#    if _D(records[-1]['Time']/1000) == '2020-01-25 00:00:00':
#        Log("records[-1]",records[-1])





    if opensign | addsign:
        if acct.Balance >= (ticker['Last']+10)*unit and unit >0:
            id = exchange.Buy(ticker['Last']+10,unit)
            orderinfo = exchange.GetOrder(id)
            data = {'ordertime':_D(records[-1]['Time']/1000),'id':id,'price':records[-1]['Close']}
            hisorder = hisorder.append(data,ignore_index=True)
            Log('买入后，最新账户信息：', exchange.GetAccount())
            Log("opensign",opensign,"addsign",addsign)
    #    else:
    #        Log('余额已不足，请充值......', exchange.GetAccount())
    if stopsign | closesign:
        exchange.Sell(-1, acct.Stocks+acct.FrozenStocks)
        data = {'ordertime':[],'id':[],'price':[]}
        hisorder = pd.DataFrame(data)
        Log('卖出后，最新账户信息：', exchange.GetAccount())
        Log("stopsign",stopsign,"closesign",closesign)

    

    
def main():
    while True:
        turtle()
        Sleep(fresh_rete*60*60*1000)        
```

> Detail

https://www.fmz.com/strategy/186598

> Last Modified

2020-03-06 12:04:41
