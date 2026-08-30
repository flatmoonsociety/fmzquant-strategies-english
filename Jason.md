
> Name

Iceberg commissioned buying-Jason
> Author

Jason_MJ

> Strategy Description

**1. Prerequisite:**
    Learning writing strategies for the first time - iceberg commission:
    This article mainly refers to the big man’s strategy: https://www.fmz.com/strategy/188435
It's basically the same as the boss's strategy, but the writing is a little rougher. Mainly used for learning introduction. Please give me some advice
**2. Antecedents**
    When buying or selling digital currencies in large amounts, the market price of the currency you want to buy/sell may be affected due to the large transaction amount. This is even more true for digital currencies with poor liquidity. A large buy order can **pull the market**, and a large sell order can **smash the market**.
    ①Pulling: Pulling up the price and raising the currency price
    ②Selling the currency: regardless of the price, sell the currency directly, causing the currency price to fall.
    ③Trading currency Stocks: The currency used for trading, taking the BTC/USDT trading pair as an example, **BTC is the trading currency**
    ④ Pricing currency Balance: The currency that users denominated, take the BTC/USDT trading pair as an example, **USDT is the pricing currency**
**Iceberg Commission:**
    Operation: refers to automatically splitting a large order into **multiple orders**, and automatically placing small orders based on the current latest buy/sell price and the price strategy set by the customer. **When the previous order is fully traded or the latest price deviates significantly from the current order, the order is automatically re-placed**
    Effect: Reduce the impact of large buy/sell orders on the market price. When making large purchases, you can **prevent your own buying costs from increasing due to price increases** due to large buy orders; when selling large amounts, you can **prevent your selling profits from lowering prices due to large sell orders**
**Data parameter comparison:**
1. Order price = latest buying price X (1-order depth)
2. Actual market order depth = (last transaction price - last order price) / last order price
3. Random single purchase quantity = average single purchase quantity X (100 - single average floating point number) % + (single average floating point number X2) %
4. Available amount = Take the account denominated currency, a random single purchase quantity, and the minimum remaining total purchase amount.
5. Purchase quantity = available amount / commission price
6. Total remaining purchase amount = total purchase amount - (initial account denominated currency - account denominated currency)

**Rules:**
1. The order is automatically canceled when the distance between the latest transaction price and the order exceeds the order depth X2 (indicating that the deviation is too large)
2. Stop the order when the total trading volume of the strategy equals the total order quantity
3. Stop the order if the latest transaction price is higher than the maximum buying price
4. Restore the order when the latest transaction price is lower than the maximum buying price
**Main parameters:**
1. Purchase amount
2. Single purchase quantity
3. Depth of commission
4. Maximum price
5. Price polling interval
6. Single purchase quantity average floating point number
7. Minimum transaction volume
**Idea:**
1. Get all unfilled orders and cancel orders
2. Get the initial account balance and determine whether it is greater than the total purchase amount.
3. Calculate the order price
4. Calculate single purchase quantity
5. Calculate available amount
6. Calculate purchase quantity
7. Execute buy
8. Take a designated break
9. Determine whether the last order was purchased successfully
10. Successful output log
11. Failure to judge whether the deviation is too large. If it is too large, it needs to be cancelled.
**Suggestion**
1. It is recommended to use ETH_USDT backtesting
**The strategy is not perfect, I hope the bosses passing by can give me some advice**
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|buyAmount|10000|Buy Amount|
|buyNum|100|Average single purchase quantity|
|depthStatus|0.1|Delegation depth|
|highPrice|20000|Highest Price|
|priceInterval|true|Ask price interval|
|minBuyNum|0.0001|Minimum transaction volume|
|buyOncePoint|10|Average floating point number of single purchase quantity|

> Source (python)

``` python
import random


def main():
    # 获取账户所有未成交订单
    Log("取消所有未成交订单")
    orders = _C(exchange.GetOrders)
    if len(orders) > 0:
        for i in range(len(orders)):
            exchange.CancelOrder(orders[i]["Id"])
            Sleep(priceInterval*1000)

    # 对比账户余额
    Log("获取用户初始化账户")
    initAccount = _C(exchange.GetAccount)
    if initAccount["Balance"] < buyAmount:
        Log("账户余额不足")
        return
    
    #比较单笔购买数量均值*市场买一价是否大于账户余额
    ticker = _C(exchange.GetTicker)
    if (ticker['Last'] * buyNum) > initAccount['Balance']:
        Log("单次购买均值价格大于账户余额，请调整参数")
        return

    lastBuyPrice = 0

    while (True):
        Sleep(priceInterval*1000)
        #获取账户信息
        account = _C(exchange.GetAccount)
        #获取当下行情
        ticker = _C(exchange.GetTicker)
        # 上次购买价格不为空，查看订单是否完成，没有完成则取消
        if lastBuyPrice > 0:
            orders1 = exchange.GetOrders()
            if len(orders1) > 0:
                for j in range(len(orders1)):
                    #计算实际市场委托深度
                    if ticker["Last"] > lastBuyPrice and ((ticker["Last"] - lastBuyPrice)/lastBuyPrice) > (2* (depthStatus/100)):
                        Log("委托价格偏离过多，最新成交价:",ticker["Last"],"委托价",lastBuyPrice)
                        exchange.CancelOrder(orders1[j]["Id"])
                        lastBuyPrice = 0
                continue
            else:
                Log("买单完成, 累计花费:", _N(initAccount["Balance"] - account["Balance"]), "平均买入价:", _N((initAccount["Balance"] - account["Balance"]) / (account["Stocks"] - initAccount["Stocks"])))
                lastBuyPrice = 0
                continue     
        else:
            Log("剩余余额:",account["Balance"])
            #委托价格 = 最新买一价*（1-委托深度/100）
            entrustPrice = _N(ticker["Buy"]*(1-depthStatus/100))
            Log("委托价格：",entrustPrice)
            #判断委托价格是否大于最高价格限定
            if entrustPrice > highPrice:
                continue
            #随机购买数量 = 单次购买数量均值 * ((100-单次均值浮点数)/100)+(单次均值浮点数*2 /100* 单次购买数量均值 *随机数0~1)  
            randomBuyNum = (buyNum*((100-buyOncePoint)/100))+(buyOncePoint*2/100 *buyNum*random.random())
            #可用数量金额 
            useMoney = min(account["Balance"],randomBuyNum,buyAmount - (initAccount["Balance"] - account["Balance"]))
            #购买数量
            orderBuyNum = _N(useMoney/entrustPrice)
            Log("交易数量：",orderBuyNum)
            #判断是否小于最小交易量
            if orderBuyNum < minBuyNum:
                break
            #因为要扣手续费，所以大概为账户99.7%
            if (entrustPrice*orderBuyNum)>(account["Balance"]*0.997):
                Log("金额为",(entrustPrice*orderBuyNum))
                Log("账户余额为",(account["Balance"]))
                continue
            #更新上次购买价格
            lastBuyPrice = entrustPrice
            #下单
            exchange.Buy(entrustPrice,orderBuyNum)
            
    account = _C(exchange.GetAccount)  
    Log("冰山委托买单完成,共计花费：",_N(initAccount["Balance"]-account["Balance"]),"平均单价为:",_N((initAccount["Balance"]-account["Balance"])/(account["Stocks"]-initAccount["Stocks"])))        

```

> Detail

https://www.fmz.com/strategy/271475

> Last Modified

2021-04-16 10:26:23
