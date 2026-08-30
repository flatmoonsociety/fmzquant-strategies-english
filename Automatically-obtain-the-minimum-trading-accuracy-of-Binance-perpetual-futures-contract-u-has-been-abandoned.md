
> Name

Automatically obtain the minimum trading accuracy of Binance perpetual futures contract u has been abandoned
> Author

GCC

> Strategy Description

Originally, it was a very reasonable approach to directly obtain the transaction accuracy from the transaction rules, but Binance often did not update this part in time, so it gave up.


> Source (python)

``` python
def init():
    global symbols, min_value
    # 获取交易规则
    exchange.SetBase('https://dapi.binance.com')
    rule = exchange.IO("api", "GET", "/dapi/v1/exchangeInfo", "", "")["symbols"]
    Log(rule)
    # 获取交易对名称
    for i in range(len(exchanges)):
        exchanges[i].SetMarginLevel(M)
        exchanges[i].SetContractType("swap")  # 设置永续合约
        _symbol = exchanges[i].GetCurrency().split("_")[0]   # +'USDT'币本位交易对名称
        # 设置交易精度
        j = 0
        flag1 = False
        flag2 = False
        #Log(rule)
        while (j < len(rule)) and flag1 == False and flag2 == False:
            if str(rule[j]["symbol"]).rfind(_symbol)>=0:
                for x in rule[j]["filters"]:
                    if x["filterType"] == "PRICE_FILTER" and flag1 == False:
                        #Log("价格",x["tickSize"])
                        #Log(len(str(float(x["tickSize"])).split('.')[-1]))
                        price_precision = len(str(float(x["tickSize"])).split('.')[-1])
                        flag1 = True
                    elif x["filterType"] == "LOT_SIZE" and flag2 == False:
                        amount_precision = len(x["minQty"].split('.')[-1])
                        flag2 = True
            j = j + 1
        exchanges[i].SetPrecision(price_precision, amount_precision)
    Log("初始化结束")
```

> Detail

https://www.fmz.com/strategy/322632

> Last Modified

2021-11-12 15:44:44
