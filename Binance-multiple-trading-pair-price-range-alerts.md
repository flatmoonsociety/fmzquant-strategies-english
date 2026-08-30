
> Name

Binance multiple trading pair price range alerts
> Author

light cloud
> Strategy Description

Because the IOS version of Aicoin is not a member, it cannot be used, and there is no price reminder, so I thought about getting one myself.
But I really didn’t understand the code, so I copied and pasted Mengda’s code, https://www.fmz.com/digest-topic/8512
My English is not good, so I use pinyin for the upper and lower limits, and the other English ones are copied from Mengda. [baring teeth]
Thank you Mengda [clasp your fists] [shake hands]! ! !
If you know of any other apps that can remind you of prices like Aicoin, please tell me. Thank you.
This default is for contract trading and supports USDT BUSD. Set the upper and lower limits. If the latest price is higher than the upper limit or lower than the lower limit, a message notification will be sent.
If you need spot trading, just remove the check mark of [Contract Trading] in the parameters. Then add the exchange and select the current currency.
FMZ needs to be bound and pushed. I bound it to QQ mailbox, and then set a special reminder tone in QQ mailbox and bound WeChat at the same time, and there will be two reminders.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|B_sleeptime|30|Polling time (seconds)|
|symbols|ETH_BUSD,ETC_USDT,LTC_USDT|Trading pairs|
|B_shangxian|3000,100,200|Price limit|
|B_xiaxian|2000,50,100|Lower price limit|
|B_heyue|true|Contract trading|

> Source (javascript)

``` javascript
var arrSymbols = symbols.split(",")
var arrshangxian = B_shangxian.split(",")
var arrxiaxian = B_xiaxian.split(",")
var shang = parseFloat(arrshangxian[i])
var xia = parseFloat(arrxiaxian[i])

function main() {
    if (B_chongzhi) {
        LogReset()
        LogVacuum()
        Log("重置所有数据", "#FF0000")
    }
    while (true) {
        for (var i = 0; i < arrSymbols.length; i++) {
            var symbol = arrSymbols[i]
            if (B_heyue == true) {
                exchange.SetContractType("swap")
            }
            exchange.SetCurrency(symbol)
            var ticker = _C(exchange.GetTicker).Last
            Log("交易对：", symbol, "最新价：", ticker)
            if (ticker > shang || ticker < xia) {
                Log(symbol, "价格跳出区间，当前最新价格：", ticker, "#FF0000", "@")
            }
            Sleep(B_sleeptime * 1000)
        }
        Sleep(5 * 1000)

    }
}
```

> Detail

https://www.fmz.com/strategy/342165

> Last Modified

2022-04-21 22:45:14
