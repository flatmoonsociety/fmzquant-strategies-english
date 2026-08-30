
> Name

Example - Scheduled testing of WeChat message push
> Author

Inventor Quantification-Little Dream
> Strategy Description

Regular test of WeChat message push example ~ To provide inspiration for users to refer to and learn from.


> Source (javascript)

``` javascript
function main(){
    var initTime = (new Date()).getTime() ;
    Log("程序起始时间：",$.getTimeByNormal(initTime) );
    var preDif = 0;
    var str = "";
    while(true){
        var nowTime = (new Date()).getTime();
        if(  Math.floor((nowTime - initTime) / (1000*60*10) ) !== preDif ){
            str = $.getTimeByNormal(nowTime);
            Log("从程序开始执行，已过10分钟！提醒。"+"--现在时间："+str+"推送微信@" );
            preDif = Math.floor((nowTime - initTime) / (1000*60*10) ) ;
        }
        Sleep(2000); 
    }
}
```

> Detail

https://www.fmz.com/strategy/15098

> Last Modified

2017-01-04 12:00:55
