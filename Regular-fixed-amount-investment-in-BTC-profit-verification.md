
> Name

Regular fixed amount investment in BTC profit verification
> Author

Brother Chun
> Strategy Description

Purchase Bitcoin for a fixed amount each time and hold it
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|FIXED_AMOUNT|100|How much RMB you buy each time|
|PERIOD|86400|Period (unit seconds)|

> Source (javascript)

``` javascript

var total_cny = 0;
var days = 0;
var total_btc = 0;

function main() {
    
    var chart = createChart();
    while( true) {
        total_cny+=FIXED_AMOUNT;
        days++;
    
        var ticker = exchange.GetTicker();
        total_btc += FIXED_AMOUNT/ticker.Last;
    
        var current_value = ticker.Last * total_btc;
    
        LogProfit(current_value - total_cny);
        
        var time = new Date().getTime();
        chart.add([0, [time, total_cny ]]);
        chart.add([1, [time, current_value]]);
        
        Sleep(PERIOD*1000);
    }
}



function createChart() {

    var options = {
        rangeSelector: {
            selected: 4
        },
        __isStock: true,
        yAxis: {
            labels: {
                formatter: function () {
                    return (this.value > 0 ? ' + ' : '') + this.value + '%';
                }
            },
            plotLines: [{
                value: 0,
                width: 2,
                color: 'silver'
            }]
        },

        plotOptions: {
            series: {
                compare: 'percent'
            }
        },

        tooltip: {
            pointFormat: '<span style="color:{series.color}">{series.name}</span>: <b>{point.y}</b> ({point.change}%)<br/> {point.text}',
            valueDecimals: 2
        },

        series: [ 
        {
            name: '成本',
            data: []
        },
           {
            name: '账户价值',
            data: []
        }
        ]
    };

    return Chart(options);
}



```

> Detail

https://www.fmz.com/strategy/16845

> Last Modified

2016-06-17 01:00:11
