
> Name

OK Confirm that the currency trading pair cannot be withdrawn
> Author

daniaoren

> Strategy Description

For personal use, simply list all the coins that cannot be withdrawn from OKEX at present. Sometimes it is very useful and you need to withdraw it yourself.


> Source (javascript)

``` javascript
function main() {
    var results = exchange.IO("api", "GET", "/api/account/v3/currencies", "" , "");
    var blacklist = []
    i = 0;
    var statusMsg = '';
	while (true)
    {
        if (results[i]["can_withdraw"] == "0"){
            Log(results[i]["currency"],"|",results[i]["name"], results[i]["can_deposit"]);
            statusMsg += results[i]["currency"] + " | " + results[i]["name"] + ' ' + results[i]["can_deposit"] + '\n';
            blacklist.push(results[i]);
        }
        i++;
        if (i >= results.length){
        	break;
        }
    }
    Log(blacklist.length);
    statusMsg = blacklist.length + '\n' + statusMsg;
    LogStatus(statusMsg);
    return blacklist;

}
```

> Detail

https://www.fmz.com/strategy/253278

> Last Modified

2021-02-10 15:29:08
