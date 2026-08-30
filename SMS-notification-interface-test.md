
> Name

SMS notification interface test
> Author

Zero

> Strategy Description

To test the SMS notification interface, please register an account on an SMS platform that supports APIs (SMS treasure is recommended), and then enter the sent URL into the interface.
For example http://www.xxxx.com/sms.php?phone=1111111&c={BODY}
Test whether you can get text messages
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|SMSAPI|http://|短信接口|
|Msg|Hello, test successful|Message sent|

> Source (javascript)

``` javascript
function main() {
    if (SMSAPI.length > 10 && SMSAPI.indexOf('http') == 0 && SMSAPI.indexOf('{BODY}') != -1) {
        Log('发送: ', Msg);
        HttpQuery(SMSAPI.replace('{BODY}', encodeURIComponent(Msg)));
        Log('发送完成, 请检测是否收到短信');
    } else {
        Log('参数配置错误, 请重新检测短信接口');
    }
}
```

> Detail

https://www.fmz.com/strategy/653

> Last Modified

2014-09-25 17:35:46
