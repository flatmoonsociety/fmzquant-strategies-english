
> Name

Single-point sniping high-frequency automatic backhand unblocking algorithm-V12
> Author

Zero

> Strategy Description

Open a position first, then specify a profit point to close the position. If the position cannot be closed and the stop-loss point is exceeded, add another position to bring down the low price until you make a profit. If you add to the position until you run out of money or more coins are added, you start to backhand. If you were originally short, you backhand to go long, and this repeats. You can also disable the automatic backhand and let the program wait for unwinding.
For example, if you open a long position with an average price of 10 yuan and the target profit is 5 cents, the program will place a sell order of 10.5 yuan. If the price drops, you will add a position near the current price, adjust the average price, and place a target profit order. If it still doesn't work, you will continue to increase the position to lower the average price. If it doesn't work, and you are trapped, you will backhand and start a short order.
Automatic backhand mechanism of strategy
If you are currently doing a long position and you are out of profit, you will automatically open a long position again. If you are trapped, you will take the currency backhand and make a short position. After the short position is profitable, you will continue to be a short position until you can no longer add to the position. Then you will backhand and start a long position. This cycle continues. As long as it was profitable last time, it will keep the direction of the last opening.
The strategy will automatically calculate the size of the required position and the new value of the target profit point.
Need to pay attention
This strategy has a complete recovery mechanism that can be practiced or learned to use.
The premise for this strategy to make 100% profit is: you must prepare enough funds to add a position
If there is not enough funds, let the automatic backhand operation occur, which will result in floating profits and losses.
If you have enough funds, you don’t need to automatically backhand, just let the program add positions all the time.
The strategy can realize high-frequency handicap strategies by adjusting parameters.
It is not suitable for futures. It is easy to liquidate the position of futures, so it can only be operated with spot goods.
The purpose of open source
Attract more people to join the communication circle of quantitative trading instead of working behind closed doors all day long
V1.1 solves the bug that caused the program to get stuck due to OKCoin freezing 0.0001 coins.
For more detailed instructions, go to: https://www.fmz.com/#!/bbs-topic/38
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|OpType|0|First opening direction: long|short|
|OpAmount|0.1|Open position quantity|
|OpMode|0|Opening method: take order|pending order|
|MaxSpace|0.5|Pending order failure distance|
|SlidePrice|0.1|Sliding price of order (yuan)|
|MaxAmount|0.3|Maximum single order amount for opening a position|
|AddGoal|true|Additional distance (yuan)|
|AddLine|0.8|Average price target for adding positions (yuan)|
|ProfitGoal|0.5|Close target (yuan)|
|Interval|true|Polling interval (seconds)|
|RestoreIt|false|Restore Progress|
|RestoreType|0|Position direction: long|short|
|RestorePrice|false|Average position price|
|RestoreAmount|false|Position quantity|
|RestoreProfit|false|Last profit|
|SaveLocal|false|Save local logs|
|AutoReverse|true|Auto backhand|
|MinStock|0.01|Minimum number of transaction coins|

> Source (javascript)

``` javascript

var TradeType = OpType == 0 ? ORDER_TYPE_BUY : ORDER_TYPE_SELL;
var OrgAccount = null;
var Counter = {s : 0, f: 0};
var LastProfit = 0;
var AllProfit = 0;
var LastTicker = null;
function _N(v, precision) {
    if (typeof(precision) != 'number') {
        precision = 4;
    }
    var d = parseFloat(v.toFixed(Math.max(10, precision+5)));
    s = d.toString().split(".");
    if (s.length < 2 || s[1].length <= precision) {
        return d;
    }

    var b = Math.pow(10, precision);
    return Math.floor(d*b)/b;
}

function EnsureCall(e, method) {
    var r;
    while (!(r = e[method].apply(this, Array.prototype.slice.call(arguments).slice(2)))) {
        Sleep(Interval);
    }
    return r;
}

function StripOrders(e, orderId) {
    var order = null;
    if (typeof(orderId) == 'undefined') {
        orderId = null;
    }
    while (true) {
        var dropped = 0;
        var orders = EnsureCall(e, 'GetOrders');
        for (var i = 0; i < orders.length; i++) {
            if (orders[i].Id == orderId) {
                order = orders[i];
            } else {
                var extra = "";
                if (orders[i].DealAmount > 0) {
                    extra = "成交: " + orders[i].DealAmount;
                } else {
                    extra = "未成交";
                }
                e.CancelOrder(orders[i].Id, orders[i].Type == ORDER_TYPE_BUY ? "买单" : "卖单", extra);
                dropped++;
            }
        }
        if (dropped == 0) {
            break;
        }
        Sleep(300);
    }
    return order;
}

function updateProfit(e, account, ticker) {
    if (typeof(account) == 'undefined') {
        account = GetAccount(e);
    }
    if (typeof(ticker) == 'undefined') {
        ticker = EnsureCall(e, "GetTicker");
    }
    var profit = (((account.Stocks + account.FrozenStocks) - (OrgAccount.Stocks + OrgAccount.FrozenStocks)) * ticker.Last) + ((account.Balance + account.FrozenBalance) - (OrgAccount.Balance + OrgAccount.FrozenBalance));
    LogProfit(_N(profit + LastProfit, 4), "币数:", _N(account.Stocks + account.FrozenStocks, 4), "钱数:", _N(account.Balance + account.FrozenBalance, 4));
}


var preMsg = "";
function GetAccount(e, waitFrozen) {
    if (typeof(waitFrozen) == 'undefined') {
        waitFrozen = false;
    }
    var account = null;
    var alreadyAlert = false;
    while (true) {
        account = EnsureCall(e, "GetAccount");
        if (!waitFrozen || (account.FrozenStocks < MinStock && account.FrozenBalance < 0.01)) {
            break;
        }
        if (!alreadyAlert) {
            alreadyAlert = true;
            Log("发现账户有冻结的钱或币", account);
        }
        Sleep(Interval);
    }
    msg = "成功: " + Counter.s + " 次, " + (AutoReverse ? "被":"解") + "套: " + Counter.f + " 次, 当前账户 钱: " + account.Balance + " 币: " + account.Stocks;
    if (account.FrozenStocks > 0) {
        msg += " 冻结的币: " + account.FrozenStocks;
    }
    if (account.FrozenBalance > 0) {
        msg += " 冻结的钱: " + account.FrozenBalance;
    }

    if (LastTicker != null && OrgAccount != null && OrgAccount != null) {
        var profit = (((account.Stocks + account.FrozenStocks) - (OrgAccount.Stocks + OrgAccount.FrozenStocks)) * LastTicker.Last) + ((account.Balance + account.FrozenBalance) - (OrgAccount.Balance + OrgAccount.FrozenBalance));
        msg += " 平仓盈亏: " + AllProfit + ", 浮动盈亏: " + _N(profit, 4);
        msg += " (初始账户 钱: " + OrgAccount.Balance + " 币 : " + OrgAccount.Stocks + ")";
    }
    

    if (msg != preMsg) {
        preMsg = msg;
        LogStatus(msg, "#ff0000");
    }
    return account;
}

// mode = 0 : direct buy, 1 : buy as buy1
function Trade(e, tradeType, tradeAmount, mode, slidePrice, maxAmount, maxSpace, retryDelay) {
    var initAccount = GetAccount(e, true);
    var nowAccount = initAccount;
    var orderId = null;
    var prePrice = 0;
    var dealAmount = 0;
    var diffMoney = 0;
    var isFirst = true;
    var tradeFunc = tradeType == ORDER_TYPE_BUY ? e.Buy : e.Sell;
    var isBuy = tradeType == ORDER_TYPE_BUY;
    while (true) {
        var ticker = EnsureCall(e, 'GetTicker');
        LastTicker = ticker;
        var tradePrice = 0;
        if (isBuy) {
            tradePrice = _N((mode == 0 ? ticker.Sell : ticker.Buy) + slidePrice, 4);
        } else {
            tradePrice = _N((mode == 0 ? ticker.Buy : ticker.Sell) - slidePrice, 4);
        }
        if (orderId == null) {
            if (isFirst) {
                isFirst = false;
            } else {
                nowAccount = GetAccount(e, true);
            }
            var doAmount = 0;
            if (isBuy) {
                diffMoney = _N(initAccount.Balance - nowAccount.Balance, 4);
                dealAmount = _N(nowAccount.Stocks - initAccount.Stocks, 4);
                doAmount = Math.min(maxAmount, tradeAmount - dealAmount, _N((nowAccount.Balance-10) / tradePrice, 4));
            } else {
                diffMoney = _N(nowAccount.Balance - initAccount.Balance, 4);
                dealAmount = _N(initAccount.Stocks - nowAccount.Stocks, 4);
                doAmount = Math.min(maxAmount, tradeAmount - dealAmount, nowAccount.Stocks);
            }
            if (doAmount < MinStock) {
                break;
            }
            prePrice = tradePrice;
            orderId = tradeFunc(tradePrice, doAmount);
        } else {
            if (Math.abs(tradePrice - prePrice) > maxSpace) {
                orderId = null;
            }
            var order = StripOrders(exchange, orderId);
            if (order == null) {
                orderId = null;
            }
        }
        Sleep(retryDelay);
    }

    if (dealAmount <= 0) {
        return null;
    }

    return {price: _N(diffMoney / dealAmount, 4), amount: dealAmount};
}

function loop(isFirst) {
    var minStock = MinStock;
    var initAccount = GetAccount(exchange, true);
    Log(initAccount);
    var holdPrice = 0;
    var holdAmount = 0;
    if (RestoreIt && isFirst) {
        LastProfit = RestoreProfit;
        TradeType = RestoreType == 0 ? ORDER_TYPE_BUY : ORDER_TYPE_SELL;
        holdPrice = RestorePrice;
        holdAmount = RestoreAmount;
        if (holdAmount != 0) {
            initAccount = {
                Stocks: initAccount.Stocks,
                FrozenStocks: initAccount.FrozenStocks,
                Balance: initAccount.Balance,
                FrozenBalance: initAccount.FrozenBalance,
            };
            if (RestoreType == 0) {
                initAccount.Stocks -= holdAmount;
                initAccount.Balance += (holdPrice * holdAmount);
            } else {
                initAccount.Stocks += holdAmount;
                initAccount.Balance -= (holdPrice * holdAmount);
            }
            OrgAccount = initAccount;
            Log("恢复持仓状态为:", RestoreType == 0 ? "做多" : "做空", "均价:", holdPrice, "数量:", holdAmount);
            if (RestoreType == 0) {
                holdAmount = Math.min(initAccount.Stocks, holdAmount);
            }
        }
        if (LastProfit != 0) {
            AllProfit = LastProfit;
            LogProfit(LastProfit, "恢复上次盈利");
        }
    }
    if (holdAmount == 0) {
        var obj = Trade(exchange, TradeType, OpAmount, OpMode, SlidePrice, MaxAmount, MaxSpace, Interval);
        if (!obj) {
            throw "出师不利, 开仓失败";
        } else {
            Log(TradeType == ORDER_TYPE_BUY ? "开多仓完成" : "开空仓完成", "均价:", obj.price, "数量:", obj.amount);
        }
        Log(GetAccount(exchange, true));
        holdPrice = obj.price;
        holdAmount = obj.amount;
    }
    var openFunc = TradeType == ORDER_TYPE_BUY ? exchange.Buy : exchange.Sell;
    var coverFunc = TradeType == ORDER_TYPE_BUY ? exchange.Sell : exchange.Buy;
    var isFinished = false;
    while (!isFinished) {
        var account = GetAccount(exchange, true);
        var openAmount = 0;
        var openPrice = 0;
        var coverPrice = 0;
        var canOpen = true;

        if (TradeType == ORDER_TYPE_BUY) {
            var upLine = AddLine;
            openPrice = _N(holdPrice - AddGoal, 4);
            openAmount = _N((holdAmount * (holdPrice - openPrice - upLine)) / upLine, 4);
            coverPrice = _N(holdPrice + ProfitGoal, 4);
            if (_N(account.Balance / openPrice, 4) < openAmount) {
                Log("没有钱加多仓, 需要加仓: ", openAmount, "个");
                if (AutoReverse) {
                    return holdAmount;
                } else {
                    canOpen = false;
                }
            }
        } else {
            var upLine = -AddLine;
            openPrice = _N(holdPrice + AddGoal, 4);
            coverPrice = _N(holdPrice - ProfitGoal, 4);
            openAmount = _N((holdAmount * (holdPrice - openPrice - upLine) / upLine), 4);
            if (account.Stocks < openAmount) {
                Log("没有币加空仓, 需要币:", openAmount);
                if (AutoReverse) {
                    return holdAmount;
                } else {
                    canOpen = false;
                }
            }
        }
        if (holdAmount < minStock) {
            Log("剩余币数过小, 放弃操作", holdAmount);
            return 0;
        }
        openAmount = Math.max(minStock, openAmount);

        var order_count = 0;
        var openId = null;
        var coverId = null;
        if (!canOpen) {
            openId = -1;
            Log("进入等待解套模式");
        }

        for (var i = 0; i < 10; i++) {
            if (!openId) {
                openId = openFunc(openPrice, openAmount);
            }
            if (!coverId) {
                coverId = coverFunc(coverPrice, holdAmount);
            }
            if (openId && coverId) {
                break;
            }
            Sleep(Interval);
        }
        if (!openId || !coverId) {
            StripOrders(exchange);
            throw "下单失败";
        }
        if (openId > 0) {
            order_count++;
        }
        if (coverId > 0) {
            order_count++;
        }

        var preAccount = account;
        while (true) {
            Sleep(Interval);
            var ticker = EnsureCall(exchange, "GetTicker");
            var orders = EnsureCall(exchange, "GetOrders");
            LastTicker = ticker;
            var nowAccount = GetAccount(exchange);
            var diff = nowAccount.Stocks + nowAccount.FrozenStocks - preAccount.Stocks;

            if (orders.length != order_count || Math.abs(diff) >= minStock) {
                StripOrders(exchange);
                nowAccount = GetAccount(exchange, true);
                //Log(nowAccount);
                var diffAmount = nowAccount.Stocks - initAccount.Stocks;
                var diffMoney = nowAccount.Balance - initAccount.Balance;
                if (Math.abs(diffAmount) < minStock) {
                    AllProfit= _N(AllProfit + (holdAmount * ProfitGoal), 4);
                    LogProfit(AllProfit, "平仓完成, 达到目标盈利点, 单次盈利", _N(holdAmount * ProfitGoal, 4));
                    initAccount = nowAccount;
                    isFinished = true;
                    if (!canOpen) {
                        Counter.f++;
                    }
                    break;
                }
                var newHoldPrice = 0;
                var newHoldAmount = 0;
                if (TradeType == ORDER_TYPE_BUY) {
                    newHoldAmount = _N(diffAmount, 4);
                    newHoldPrice = _N((-diffMoney) / diffAmount, 4);
                } else {
                    newHoldAmount = _N(-diffAmount, 4);
                    newHoldPrice = _N(diffMoney / (-diffAmount), 4);
                }
                // if open again, we need adjust hold positions's price
                var isAdd = false;
                if (newHoldAmount > holdAmount) {
                    holdPrice = newHoldPrice;
                    isAdd = true;
                }
                holdAmount = newHoldAmount;
                if (!isAdd) {
                    // reset initAccount
                    initAccount = {
                        Stocks : nowAccount.Stocks,
                        Balance : nowAccount.Balance,
                        FrozenBalance : nowAccount.FrozenBalance,
                        FrozenStocks : nowAccount.FrozenStocks,
                    };
                    if (TradeType == ORDER_TYPE_BUY) {
                        initAccount.Stocks -= holdAmount;
                        initAccount.Balance += holdAmount * holdPrice;
                    } else {
                        initAccount.Stocks += holdAmount;
                        initAccount.Balance -= holdAmount * holdPrice;
                    }
                    initAccount.Stocks = _N(initAccount.Stocks, 4);
                    initAccount.Balance = _N(initAccount.Balance, 4);
                    Log("持仓前账户调整为: ", initAccount);
                }
                Log((TradeType == ORDER_TYPE_BUY ? "多仓" : "空仓"), (isAdd ? "加仓后" : "平仓后"), "重新调整持仓, 均价: ", holdPrice, "数量", holdAmount);
                Log("买一:", ticker.Buy, "卖一:", ticker.Sell, "上次成交价:", ticker.Last);
                Log(nowAccount);
                break;
            }
        }
    }
    return 0;
}

function onexit() {
    StripOrders(exchange);
    Log("Exit");
}

function main() {
    if (AddLine > AddGoal || AddLine <= 0) {
        throw "加仓均价目标错误";
    }
    if (exchange.GetName().indexOf("Future") != -1) {
        throw "只支持现货, 期货容易爆仓, 暂不支持";
    }
    if (exchange.GetRate() != 1) {
        Log("已禁用汇率转换");
        exchange.SetRate(1);
    }
    EnableLogLocal(SaveLocal);
    Interval *= 1000;
    SetErrorFilter("502:|503:|unexpected|network|timeout|WSARecv|Connect|GetAddr|no such|reset|http|received|EOF");
    StripOrders(exchange);
    OrgAccount = GetAccount(exchange);
    var isFirst = true;
    LogStatus("启动成功");
    while (true) {
        var ret = loop(isFirst);
        isFirst = false;
        if (ret != 0) {
            Counter.f++;
            if (TradeType == ORDER_TYPE_BUY) {
                TradeType = ORDER_TYPE_SELL;
                Log("开始反手做空");
            } else {
                TradeType = ORDER_TYPE_BUY;
                Log("开始反手做多");
            }
        } else {
            Counter.s++;
        }
        Sleep(Interval);
    }
}
```

> Detail

https://www.fmz.com/strategy/2406

> Last Modified

2018-06-05 16:27:50
