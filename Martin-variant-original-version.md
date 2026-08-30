
> Name

Martin variant original version
> Author

baby dinosaur
> Strategy Description

This was my first simple strategy after entering Macau. It took me 10 minutes to write it out at the time. It is a Martin variant with a very small increase interval. The risk of liquidation is controlled through fixed investment and gradually increasing the interval. The profit and loss ratio is much better than the traditional Martin.
    During the bull market in March and April, this Martin performed very well. At its peak, he used a small amount of money to double a day. At that time, he used 12u to run CHR to 48u in four days.
    However, times have changed and the bull market is no longer there. If this Martin is used in today's market, it will inevitably make users become text message receivers, so I shared it.
    In fact, the real market still has some value that can be run, but it requires manual timing. Now it is no longer the kind of market where Martin sits and counts money at the beginning.      

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|zuoduo|true|Go long|
|zuokong|false|Short|
|CV|3|Price Accuracy|
|MarginLevel|75|Leverage multiple|
|k|true|First opening volume|
|n|true|Quantity of replenishment|
|Q|0.03|Profit stop point|
|E|0.0046|Interval of adding positions|

> Source (python)

``` python
'''backtest
start: 2021-05-01 00:00:00
end: 2021-05-14 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"EOS_USDT","balance":1000}]
args: [["zuokong",true],["n",3],["E",0.02]]
'''
def main():
    while True:
        exchange.SetContractType("swap")
        exchange.SetMarginLevel(MarginLevel)
        ticker = _C(exchange.GetTicker)
        account = _C(exchange.GetAccount)
        position = _C(exchange.GetPosition)
        if zuoduo:
            if len(position) == 0:   
                    exchange.SetDirection("buy")
                    exchange.Buy(-1, k, "开多")
            if len(position) > 0:
                if position[0].Type==0:
                    
                    if position[0].Price+Q<ticker["Last"]:
                        exchange.SetDirection("closebuy")
                        exchange.Sell(-1, position[0].Amount) 
                        account = exchange.GetAccount()
                        LogProfit(account["Balance"]) 
                    fx=(E/n)*position[0].Amount  
                    if position[0].Profit<position[0].Margin * -fx :
                        #轮询加仓
                            exchange.SetDirection("buy")
                            exchange.Buy(-1, k)
                            LogProfit(account["Balance"])     
        if zuokong:
            if len(position) == 0:   
                    exchange.SetDirection("sell")
                    exchange.Sell(-1, k, "开空")
            if len(position) > 0:
                if position[0].Type == 1 :
                    fp=Q*position[0].Amount
                    if position[0].Profit > 0.01*fp*ticker["Last"] :
                        exchange.SetDirection("closesell")
                        exchange.Buy(-1, position[0].Amount) 
                        account = exchange.GetAccount()
                        LogProfit(account["Balance"]) 
                    fx=(E/n)*position[0].Amount  
                    if position[0].Profit<position[0].Margin * -fx :
                        #轮询加仓
                            exchange.SetDirection("sell")
                            exchange.Sell(-1, n)
                            LogProfit(account["Balance"])
        
        Sleep(3000)
```

> Detail

https://www.fmz.com/strategy/293373

> Last Modified

2022-03-02 15:39:53
