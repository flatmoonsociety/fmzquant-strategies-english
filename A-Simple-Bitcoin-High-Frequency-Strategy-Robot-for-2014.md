
> Name

A Simple Bitcoin High Frequency Strategy Robot for 2014
> Author

grass
> Strategy Description

**Introduction to Strategy**
Strategy sharing address:
https://www.fmz.com/strategy/1088
This strategy has been my main strategy since I started making virtual currency. After continuous improvement and modification, it has become much more complicated, but the main idea has not changed. The version I shared is the initial version without obvious bugs. It is the simplest and clearest. There is no position management, every transaction is full, there is no restart after death, etc., but it is enough to explain the problem.
The strategy ran from August 2014 until the beginning of this year when the exchange charged fees. It ran pretty well during this period, with very few losses. The funds went from the initial 200 yuan to 80 bitcoins. For the specific process, you can read the series of articles in [Xiao Cao’s Sina Blog] (http://blog.sina.com.cn/u/2389357153) [The Road to Automated Trading of Virtual Currency] (http://blog.sina.com.cn/s/blog_8e6ab2610102v6sq.html).
**Why share this strategy**
1. After the exchange charges handling fees, it almost kills all high-frequency strategies, and mine is no exception. But it may still work after changing the strategy, so you can study it.
2. It’s been a long time since I’ve shared anything, and I’ve wanted to write this article for a long time.
3. Communicate and learn with everyone.
**Principles of Strategy**
The principle of this strategy is extremely simple. It can be understood as a quasi-high-frequency market-making strategy. You may want to beat others after reading it. This can make money. At that time, almost anyone could write it. I didn't expect it to be so effective at first. It shows that if you have an idea in your mind, you have to put it into practice quickly. There may not be any unexpected surprises. In 2014, when Bitcoin bots were emerging, it was too easy to write strategies to make money.
Like all high-frequency strategies, this strategy is also based on orderbook. The following figure shows the order distribution of a typical Bitcoin exchange.
 https://dn-filebox.qbox.me/0d8ec18c831404d3d1c19e17299c78017abcfd48.png
You can see that the left side is the buy order, which shows the number of pending orders at different prices, and the right side is the sell order. It can be imagined that if a person wants to buy Bitcoin, if he does not want to place an order and wait, he can only choose to take the order. If he has a lot of orders, a large number of sell orders and pending orders will be completed, which will have an impact on the price. However, this impact generally does not last forever. There are still people who want to take orders and sell, and the price is likely to recover in a very short period of time. On the other hand, it is similar to understand that someone wants to sell coins.
Take the pending order in the picture as an example. If you want to buy 5 coins directly, the price will reach 10377. At this time, if someone wants to sell 5 coins directly, the price will reach 10348. This space is the profit space. The strategy will be discussed later. If you place an order at a price lower than 10377, such as 10376.99, you will also buy at a price slightly higher than 10348, such as 10348.01. If the situation just happened, you will obviously earn the price difference. Although it won't be perfect every time, under the influence of probability, the chance of making money is actually surprisingly high.
Let’s use the parameters of the current strategy to explain the specific operation. Of course, this parameter cannot be used, and it is just an explanation. It will look upwards for a price with a cumulative sell order volume of 8 coins, here is 10377, then the selling price at this time is this price minus 0.01 (the amount of subtraction can be random), similarly it will look downwards for a cumulative buy pending order volume of 8 coins, here is 10348, then the selling price at this time is 10348.01, and the buying and selling price at this time is The price difference is 10376.99-10348.01=28.98, which is greater than the strategy's preset price difference of 1.5. The order will be placed at these two prices and waited for the transaction. If the price difference is less than 1.5, a price will be found to place the order. For example, the market price is plus or minus 10, and the order will be picked up (it is more appropriate to continue to find the depth of the long position).
**Further instructions**
1. What should I do if I have no money or coins?
This situation is very common when I have less money. Most of the time I only place one side of the order, but it is not a big problem. In fact, the logic of currency balance can be added, but losses will inevitably occur in the balancing process. After all, every transaction is favored by probability. I chose to wait for the transaction on one side. Of course, this also wastes the transaction opportunity on the other side.
2. How are positions managed?
In the beginning, it was all about buying and selling with a full position. Later, it was divided into different groups according to different parameters, and the transactions were not completed at once.
3. Is there no stop loss?
The strategy has a complete logic of buying and selling pending orders. I don’t think there is a need for stop loss (can be discussed). Moreover, probability is favored. Transaction is an opportunity. Stop loss is a pity.
4. How to adjust the strategy for earning coins?
The parameters at this time are symmetrical, that is, the cumulative sell order is 8 coins upward, and the cumulative buy order is 8 coins downward. It is slightly unbalanced, for example, it is changed to the cumulative sell order 15 coins, making the opportunity to sell coins more rare, and there is a greater chance that it will be bought back at a lower price. In this way, coins will be earned, and in turn, money will be made. In fact, the early stage strategy is so effective that both coins and money increase.
**Code explanation**
The complete code can be found in my strategy sharing at www.fmz.com. Only the core logic functions are explained here. Without any changes, the simulation disk that comes with botvs is running completely normally. This is a strategy from more than 3 years ago, and the platform still supports it, which is so touching.
The first is to obtain the buying and selling price function GetPrice(), which needs to obtain the order depth information. Note that the length of the order depth information on different platforms is different, and even if all orders are traversed, the required amount is still not available (many 0.01 grid pending orders will cause this situation in the later period). Calling GetPrice('Buy') is to obtain the buying price.
```
function GetPrice(Type) {
   //_C()是平台的容错函数
    var depth=_C(exchange.GetDepth);
    var amountBids=0;
    var amountAsks=0;
    //计算买价，获取累计深度达到预设的价格
    if(Type=="Buy"){
       for(var i=0;i<20;i++){
           amountBids+=depth.Bids[i].Amount;
           //参数floatamountbuy是预设的累计深度
           if (amountBids>floatamountbuy){
               //稍微加0.01，使得订单排在前面
              return depth.Bids[i].Price+0.01;}
        }
    }
    //同理计算卖价
    if(Type=="Sell"){
       for(var j=0; j<20; j++){
    	   amountAsks+=depth.Asks[j].Amount;
            if (amountAsks>floatamountsell){
            return depth.Asks[j].Price-0.01;}
        }
    }
    //遍历了全部深度仍未满足需求，就返回一个价格，以免出现bug
    return depth.Asks[0].Price
}
```
The main function of each loop is onTick(). The loop time set here is 3.5s. Each loop will cancel the original order and re-place the order. The simpler it is, the less likely it is to encounter bugs.
```
function onTick() {
    var buyPrice = GetPrice("Buy");
    var sellPrice= GetPrice("Sell");
    //diffprice是预设差价，买卖价差如果小于预设差价，就会挂一个相对更深的价格
    if ((sellPrice - buyPrice) <= diffprice){
            buyPrice-=10;
            sellPrice+=10;}
    //把原有的单子全部撤销，实际上经常出现新的价格和已挂单价格相同的情况，此时不需要撤销
    CancelPendingOrders() 
    //获取账户信息，确定目前账户存在多少钱和多少币
    var account=_C(exchange.GetAccount);
    //可买的比特币量，_N()是平台的精度函数
    var amountBuy = _N((account.Balance / buyPrice-0.1),2); 
    //可卖的比特币量，注意到没有仓位的限制，有多少就买卖多少，因为我当时的钱很少
    var amountSell = _N((account.Stocks),2); 
    if (amountSell > 0.02) {
        exchange.Sell(sellPrice,amountSell);}
    if (amountBuy > 0.02) {
        exchange.Buy(buyPrice, amountBuy);}
    //休眠，进入下一轮循环
    Sleep(sleeptime);
}
```

**Tail**
The whole program only has more than 40 lines, which seems very simple, but it took me more than a week at the time, and this was still on the botvs platform. The biggest advantage is that I started early. In 2014, the market was dominated by moving bricks, and there were not many high-frequency grid and market grabs, which made the strategy a fish in water. Later, the competition inevitably became more and more fierce, and I made more and more money. I faced many challenges, and I had to make major changes every once in a while to deal with it, but overall it went smoothly. When the trading platform does not charge handling fees, it is a paradise for programmed trading. Because retail investors do not charge handling fees and tend to operate, it provides room for high frequency and arbitrage. All of this basically ends with the two-way handling fees of 0.1-0.2%. It is not only a problem of being charged, but also a decrease in the activity of the entire market.
But there is still a lot of room for quantitative strategies that do not require high frequency.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|sleeptime|3500|Sleep time|
|floatamountbuy|8|Buy order depth|
|floatamountsell|8|Sell order height|
|diffprice|1.5|arbitrage spread|

> Source (javascript)

``` javascript
/*
就是我刚开始编写机器人的源代码，几乎没有改动，参数也是原来的参数。这个版本的程序有许多
需要改进的地方，但即使如此，它也当时表现除了惊人的盈利能力，在我本金不多时，不加杠杆平
均每天盈利在5%左右。当然无论从哪一方面，它都不适应今天的市场。
我同时也发了一篇文章在社区，大家可以看看。
by 小草
*/

//稍微改了一下，用了平台的容错函数_C(),和精度函数_N().
//取消全部订单
function CancelPendingOrders() {
    var orders = _C(exchange.GetOrders);
    for (var j = 0; j < orders.length; j++) {
          exchange.CancelOrder(orders[j].Id, orders[j]);}
}

//计算将要下单的价格
function GetPrice(Type,depth) {
    var amountBids=0;
    var amountAsks=0;
    //计算买价，获取累计深度达到预设的价格
    if(Type=="Buy"){
       for(var i=0;i<20;i++){
           amountBids+=depth.Bids[i].Amount;
           //floatamountbuy就是预设的累计买单深度
           if (amountBids>floatamountbuy){
               //稍微加0.01，使得订单排在前面
              return depth.Bids[i].Price+0.01;}
        }
    }
    //同理计算卖价
    if(Type=="Sell"){
       for(var j=0; j<20; j++){
    	   amountAsks+=depth.Asks[j].Amount;
            if (amountAsks>floatamountsell){
            return depth.Asks[j].Price-0.01;}
        }
    }
    //遍历了全部深度仍未满足需求，就返回一个价格，以免出现bug
    return depth.Asks[0].Price
}
 
function onTick() {
    var depth=_C(exchange.GetDepth);
    var buyPrice = GetPrice("Buy",depth);
    var sellPrice= GetPrice("Sell",depth);
    //买卖价差如果小于预设值diffprice，就会挂一个相对更深的价格
    if ((sellPrice - buyPrice) <= diffprice){
            buyPrice-=10;
            sellPrice+=10;}
    //把原有的单子全部撤销，实际上经常出现新的价格和已挂单价格相同的情况，此时不需要撤销
    CancelPendingOrders() 
    //获取账户信息，确定目前账户存在多少钱和多少币
    var account=_C(exchange.GetAccount);
    //可买的比特币量
    var amountBuy = _N((account.Balance / buyPrice-0.1),2); 
    //可卖的比特币量，注意到没有仓位的限制，有多少就买卖多少，因为我当时的钱很少
    var amountSell = _N((account.Stocks),2); 
    if (amountSell > 0.02) {
        exchange.Sell(sellPrice,amountSell);}
    if (amountBuy > 0.02) {
        exchange.Buy(buyPrice, amountBuy);}
    //休眠，进入下一轮循环
    Sleep(sleeptime);
}
    
function main() {
    while (true) {
        onTick();
    }
}
```

> Detail

https://www.fmz.com/strategy/1088

> Last Modified

2019-06-06 12:30:10
