
> Name

Heading to the opening of new coins listed on Binance
> Author

GCC

> Strategy Description

It was used to rush the opening of Binance’s new currency. Obviously, the success rate is not high. On November 4, 2021, it was used to rush the opening of DAR. I bought it at the top of the mountain. I stopped the loss in time and lost 10%. I stopped playing!
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|XX|200|How much|

> Source (python)

``` python
def main():
    Log(exchange.GetAccount())
    Log(exchange.GetCurrency())
    while True:
        ticker = exchange.GetTicker()
        if ticker:
            Log("开盘了，冲啊！！！@")
            exchange.SetPrecision(1,0)
            amount = XX/ticker['Last']
            exchange.Buy(-1, amount)
            exchange.Buy(-1, amount/2)
            exchange.Buy(-1, amount/4)
            exchange.Buy(-1, amount/8)
            exchange.Buy(-1, amount/16)
            Sleep(15*1000)
            while True:
                try:
                    _ticker = exchange.GetTicker()
                    if _ticker['Last'] > ticker['Last']:
                        exchange.Sell(-1, amount/3)
                        Log("已经卖出三分之一@")
                        return
                    else:
                        Sleep(30)
                        continue
                except:
                    Sleep(30)
                    continue
        else:
            Sleep(20)
```

> Detail

https://www.fmz.com/strategy/324178

> Last Modified

2021-11-20 13:45:47
