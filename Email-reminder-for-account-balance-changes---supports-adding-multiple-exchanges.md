
> Name

Email reminder for account balance changes - supports adding multiple exchanges
> Author

Zero

> Strategy Description

Detect changes in currency and money in the account balance and send them to the designated email address. This does not support backtesting
In the past, Fetion SMS was used, but because too many people were using it, the account was frozen and the SMS interface could no longer be used, so it was replaced by email.
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|LoopInterval|10|Detection interval (seconds)|
|AlertMode|0|Reminder mode: Change reminder|Condition alarm|Minimum value alarm|
|MaxDiffCNY|false|Minimum change in money|
|MaxDiffCoin|false|Minimum coin change|
|MinCoin|false|Coin minimum value|
|MinCNY|false|Minimum value of money|
|SMTPServer|smtp.163.com|SMTP Server|
|SMTPUser|test@163.com|Sending Email (SMTP Username)|
|SMTPPass|***|Email password (SMTP password)|
|SendMode|0|Receive email: self|other|
|DstMail|test@163.com|Recipient Email|

> Source (javascript)

``` javascript

function Notify(msg) {
    var ret = Mail(SMTPServer, SMTPUser, SMTPPass, SendMode == 0 ? SMTPUser : DstMail , msg, "余额变动 " + msg);
    if (ret) {
        Log("邮件通知成功");
    } else {
        Log("邮件通知失败");
    }
    Log(ret ? "邮件发送成功" : "邮件发送失败");
    return ret;
}

function GetAccount(print) {
    var all = {
        Balance : 0,
        Stocks  : 0,
    };
    var currency = exchange.GetCurrency();
    for (var i = 0; i < exchanges.length; i++) {
        if (exchanges[i].GetCurrency() != currency) {
            throw "币种不相同";
        }
        var account;
        while (!(account = exchanges[i].GetAccount())) {
            Sleep(1000);
        }
        all.Stocks += (account.Stocks + account.FrozenStocks);
        all.Balance += (account.Balance + account.FrozenBalance);
        if (typeof(print) != 'undefined' && print) {
            Log(exchanges[i].GetName(), "钱: ", (account.Balance + account.FrozenBalance), "币: ", (account.Stocks + account.FrozenStocks));
        }
    }

    return all;
}

function main() {
    // Disable rate auto convert
    exchange.SetRate(1);
    if (Version() < 2.7) {
        throw "只支持2.7或以上版本";
    }
    var preAccount = GetAccount(true);
    if (!Notify("策略启成功, 总钱: " + preAccount.Balance + ", 币: " + preAccount.Stocks)) {
        throw "Exit";
    }
    Log("初始信息: ", "总钱:", preAccount.Balance, "总币:", preAccount.Stocks);
    var alertAlrelady = false;
    while (true) {
        Sleep(LoopInterval * 1000);
        var account = GetAccount();
        if (AlertMode == 2) {
            if ((MinCoin > 0 && account.Stocks < MinCoin) || (MinCNY > 0 && account.Balance < MinCNY)) {
                if (!alertAlrelady) {
                    Log(account);
                    Notify(exchange.GetName() + "资金过少 总钱: " + account.Balance + ", 币: " + account.Stocks);
                    alertAlrelady = true;
                }
            } else {
                alertAlrelady = false;
            }
        } else if (account.Stocks != preAccount.Stocks || account.Balance != preAccount.Balance) {
            if (AlertMode == 0 || (MaxDiffCoin > 0 && Math.abs(account.Stocks - preAccount.Stocks) >= MaxDiffCoin) || (MaxDiffCNY > 0 && Math.abs(account.Balance - preAccount.Balance) >= MaxDiffCNY)) {
                Log(account);
                preAccount = account;
                Notify(exchange.GetName() + "账户变动为 总钱: " + account.Balance + ", 币: " + account.Stocks);
            }
        }
    }
}
```

> Detail

https://www.fmz.com/strategy/2006

> Last Modified

2014-12-24 23:22:24
