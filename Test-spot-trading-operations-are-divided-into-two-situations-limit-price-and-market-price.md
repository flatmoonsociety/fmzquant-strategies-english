
> Name

Test spot trading operations are divided into two situations: limit price and market price.
> Author

Taofen Quantification
> Strategy Description

Backtesting Huobi data and trading in the wexapp simulation, we got results similar to the following:
If the current currency type being traded is BTC_USDT, then:
To buy at a limited price, exchange.Buy(6840, 5) means buying 5 BTC at a price of 6840.
To buy at market price, exchange.Buy(-1, 5) is to buy BTC worth 5 usdt at market price. (*****Please note that this is the only special thing among the 4 cases***)
To sell at a limited price, exchange.Sell(7350, 3) is to sell 3 BTC at a price of 7350.
To sell at market price, exchange.Sell(-1, 3) is to sell 3 BTC at market price.
Strategy code: https://www.fmz.com/m/edit-strategy/191349
April 5, 2020

=====I am the low-key dividing line======
A good trading platform can make your strategy skyrocket. If you register through the link, you can get a VIP5 handling fee discount for two months:
(Spot: 0% for pending orders, 0.07% for takers. Contract: 0% for pending orders, 0.04% for takers)
https://www.kucoin.cc/ucenter/signup?rcode=1wxJ2fQ&lang=zh_CN&utmsource=VIP_TF


> Source (javascript)

``` javascript
/*backtest
start: 2020-01-01 00:00:00
end: 2020-04-01 00:00:00
period: 1d
exchanges: [{"eid":"Huobi","currency":"BTC_USD","balance":1000000,"stocks":0}]
*/

var id, order, buyAmount, lastPrice;

function main() {
    Log(exchange.GetAccount());

    lastPrice = parseInt(exchange.GetTicker().Last);
    id = exchange.Buy(lastPrice + 50, 5); // 限价买入5个BTC，买入价是当前最新价格+50          
    Log(order = exchange.GetOrder(id));
    buyAmount = parseFloat(order.DealAmount);
    Log(exchange.GetAccount());

    Sleep(1000);
    last_price = parseInt(exchange.GetTicker().Last);
    id = exchange.Sell(lastPrice - 50, buyAmount); // 限价卖出5个BTC，卖出价是当前最新价格-50    
    Log(order = exchange.GetOrder(id));
    Log(exchange.GetAccount());

    Sleep(1000);
    id = exchange.Buy(-1, 5); // 市价买入BTC，成交量是5个usdt    
    Sleep(1000);    
    Log(order = exchange.GetOrder(id));
    buyAmount = parseFloat(order.DealAmount);    
    Log(exchange.GetAccount());

    Sleep(1000);    
    id = exchange.Sell(-1, buyAmount); // 市价卖出BTC，成交量是刚才买入的BTC   
    Sleep(1000);    
    Log(order = exchange.GetOrder(id));
    Log(exchange.GetAccount());

}
```

> Detail

https://www.fmz.com/strategy/191349

> Last Modified

2021-02-05 17:09:03
