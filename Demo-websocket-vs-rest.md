
> Name

Demo speed test-websocket-vs-rest
> Author

momox

> Strategy Description

The speed test of the websocket interface and the REST interface supports adding multiple exchange tests. Note that it will temporarily increase the frequency of your api calls. Please ensure that it does not affect the operation of other robots. If the error "Futures_OP 4: argument error" occurs, please update to the latest custodian program
Special reminder: You can only add exchanges that support the websocket interface (a bit nonsense, it does not support the websocket interface, how can you test the speed), otherwise it will go wrong. Currently, Huobi provides the websocket interface, but BTCC does not. For other information, please consult the relevant exchange API introduction or help


> Source (javascript)

``` javascript


var Interval=1000;

function _N(v, precision) {



    if (typeof (precision) != 'number') {



        precision = 4;



    }



    var d = parseFloat(v.toFixed(Math.max(10, precision + 5)));



    s = d.toString().split(".");



    if (s.length < 2 || s[1].length <= precision) {



        return	d;



    }


    var b = Math.pow(10, precision);



    return	Math.floor(d * b) / b;



}




function onexit() {
   
    Log("【【【系统退出】】】");
} 


function main() {

   

	var start=Date.now();
   
    

 for (var i = 0; i < exchanges.length; i++) {


    var ecg=exchanges[i];
    //Log(ecg);
   
    ecg.IO("rest");//rest 模式
    var iii=0;
    var sum=0;
    while (iii<=10) {  //连续调用10次，取平均值
       
        var account = null;
        start=Date.now();       
        account = ecg.GetAccount();  //测试执行的API函数，可根据需要自己修改，如 GetTick
        iii=iii+1;
        if(account){
            var delay=(Date.now()-start);
            sum=sum+delay;            
             
        }




        Sleep(1000);
    
    }
     Log("平均毫秒数【"+_N(sum/iii,2)+"】"+ecg.GetName()+" rest"); 
     
     ecg.IO("websocket"); //websocket 模式
    sum=0;
    iii=0;
    while (iii<=10) {  //连续调用10次，取平均值
       
        var account = null;
        start=Date.now();       
        account = ecg.GetAccount();  //测试执行的API函数，可根据需要自己修改，如 GetTick
        iii=iii+1;
        if(account){
            var delay=(Date.now()-start);
            sum=sum+delay;            
             
        }




        Sleep(1000); 
    
    }
     Log("平均毫秒数【"+_N(sum/iii,2)+"】"+ecg.GetName()+" websocket"); 
 }
}





```

> Detail

https://www.fmz.com/strategy/7547

> Last Modified

2016-01-09 20:58:20
