
> Name

Set the Bitcoin price and push it on WeChat - 100 rounded breakthrough push
> Author

FMZ_JH

> Strategy Description

Teaching strategies:
When the price is an integer of 100, a WeChat push will be output, which will output an array containing 10 elements.
The preferred range for locking data
Poll whether the data spans this interval
Above this interval is an upward breakthrough. Compare it with the previous trigger data. If it is different, record it.
Above this interval is a downward breakthrough. If it is different from the previous trigger data, record it. Note that there is a 100 interval that needs to be added because they all fall into the bottom integer interval.
Array push forward
loop
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|Interval|true|interval|


> Source (javascript)

``` javascript
/*backtest
start: 2020-10-13 00:00:00
end: 2020-10-14 01:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"OKEX","currency":"BTC_USDT"}]
*/
var a=[1,2,3,4,5,6,7,8,9,10]
var ticker= _C(exchange.GetTicker)

function lock(){                                //锁定现价在哪个整数区间
    P=parseInt(ticker.Last/100)*100
    HP=P+100
    lock_tickLast=ticker.Last
//    Log(P,HP,ticker.Last)
} 

function stack(){
    for(var k=0;k<a.length;k++)
        a[k]=a[k+1]
}    

function onTick(){
    ticker = _C(exchange.GetTicker) 
    var get=parseInt(ticker.Last/100)*100
    if(get>P){
        a[9]=get 
        if(a[8]!=a[9]){
            str=a.toString()
            if(a[9]-a[8]>100)
                Log("向上跳空突破成功",get,ticker.Last,"{",str,"}",'@')
            else                        
                Log("向上突破成功",get,ticker.Last,"{",str,"}",'@' )
            lock()
            stack()
        }
    } 
    else if(get<P){
        a[9]=get+100
        if(a[9]!=a[8]){
            str=a.toString()
            if(a[8]-a[9]>100)
                Log("向下跳空突破成功",a[9],ticker.Last,"{",str,"}",'@')
            else
                Log("向下突破成功",a[9],ticker.Last,"{",str,"}",'@' )
            lock()
            stack()
        }
    }
}

function main(){

    lock()
    a[8]=P
//    var ticker=0
    Log("程序运行开始推送",ticker.Last,'@')
    
    while(true){ 

            onTick()  

        Sleep(Interval*1000)                      
            
    }    
}


```

> Detail

https://www.fmz.com/strategy/231955

> Last Modified

2020-10-29 15:09:21
