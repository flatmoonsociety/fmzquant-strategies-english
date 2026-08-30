
> Name

Yield statistics
> Author

Brother Chun
> Strategy Description

Statistical rate of return
BotVS's income statistics can only record one curve. Technical analysis cannot be performed. This template can automatically calculate the income, rate of return, monthly rate of return, annualized rate of return and maximum drawdown of the last 1 day, the last 1 day, the last 7 days, the last 7 days, the last 30 days, the last 30 days and all time. (The monthly and annualized returns calculated based on short time periods do not use the compound interest algorithm.)
Usage: Introduce this template and replace the LogProfit function of the original strategy with $.LogProfit.  And in the place of LogStatus, add the return string of $.ProfitSummary(initial capital)
For example:
function main() {
    while(true) {
        var t = exchange.GetTicker();
        $.LogProfit(t.Last);
        LogStatus($.ProfitSummary(10000));
        Sleep(3600000);
    }
}
Display effect:
Day 1: Closed at -78.44 yuan (-0.537%), monthly -16.781%, annualized -204.169%, retracement 1.106%
Last day: closed at 176.08 yuan (1.221%), monthly return 38.226%, annual return 465.087%, retracement 1.236%
7th: Closed 771.74 yuan (5.599%), monthly return 24.141%, annual return 293.719%, retracement 1.517%
Last 7 days: closed at 223.15 yuan (1.64%), monthly rate 7.071%, annual rate 86.039%, retracement 0.9%
30th: Closed 1570.31 yuan (12.094%), monthly return 12.111%, annual return 147.352%, retracement 3.251%
On the 30th: closed at 200.12 yuan (1.565%), monthly rate of 1.567%, annual rate of 19.076%, retracement of 1.521%
Total: 4554.11 yuan (45.541%) closed, maximum retracement 3.251%, statistical time 74 days and 23 hours
> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|SYS_LOGPROFIT|true|Whether it is also recorded to the system's own LogProfit|

> Source (javascript)

``` javascript
$.LogProfit = function(profit) {
    var args = Array.prototype.slice.call(arguments);
    if (SYS_LOGPROFIT) {
        LogProfit.apply(this, args);
    } else {
        args.unshift('收益');
        Log.apply(this,args);
    }

    var _history = $.GetAllProfit();
    _history.push([ Math.floor(new Date().getTime()/1000), profit]);
    _G('profit_history', JSON.stringify(_history));
};

$.GetAllProfit = function() {
	var old = _G('profit_history') || '[]';
    try {
    	var _history = JSON.parse(old);
    	return _history;
    } catch(e) {
    	_G('profit_history', null);
    	return [];
    }
};

function filterProfit(from, to) {
	var arr = $.GetAllProfit();
	if (!arr || arr.length === 0) return;
	var re, maxdrawback=0, lastProfit=0, maxProfit=false, maxdrawbackProfit=0;
	var earlest, latest;
	for(var i=0;i<arr.length;i++) {
		if (!arr[i]) continue;
		if (arr[i][0] > from && arr[i][0] <= to) {
			var profit = arr[i][1];
			if (!earlest) earlest = arr[i];
			latest = arr[i];
			if (!lastProfit) lastProfit = profit;
			if (maxProfit === false || maxProfit < profit) maxProfit = profit;
			var drawback = maxProfit - profit;
			if (drawback > maxdrawback) {
				maxdrawback = drawback;
				maxdrawbackProfit = maxProfit;
			}
		}
	}
	if (!earlest || !latest) return;
	return [earlest, latest, maxdrawback, maxdrawbackProfit];
}

function daysProfit(offset, days) {
	var from = getDaySecond( -offset+days);
	var to = getDaySecond(-offset);
	var arr = filterProfit( from, to );
	if (!arr || !arr[0] || !arr[1]) return;
	var profitTime = arr[1][0] - arr[0][0];
	if (!profitTime) return;
	var periodTime = to - from;
	var profit = arr[1][1] - arr[0][1];
	var realPercent = profitTime*100 / periodTime;
	var expectedProfit = profit * 100 / realPercent;
	return {
		profit:profit, 
		expectedProfit:expectedProfit,
		profitTime:profitTime,
		periodTime:periodTime,
		open: arr[0][1],
		close: arr[1][1],
		drawback: arr[2],
		drawbackProfit: arr[3]
	};
}

function getDaySecond(days) {
	var d = new Date();
	var now = d.getTime();
	now -= days*86400000;
	d.setTime(now);
	return Math.floor(d.getTime() / 1000);
} 

$.DaysProfit = function(days) {
	return filterProfit(days)[2];
};

$.ProfitSummary = function(initialBalance) {
	if (!initialBalance) return '没有传入初始资金';

	var day = daysProfit(0, 1);
	var lastDay = daysProfit(-1, 1);
	var week = daysProfit(0,7);
	var lastWeek = daysProfit(-7,7);
	var month = daysProfit(0,30);
	var lastMonth = daysProfit(-30,30);
	var all = daysProfit(0, 10000);
	if (!all) return '';
	var _days = Math.floor(all.profitTime / 86400);

	var text = [];
	var t = profitSummary(day, initialBalance);
	if (t) text.push('1日: '+t);
	t = profitSummary(lastDay, initialBalance);
	if (t) text.push('上1日: '+t);
	t = profitSummary(week, initialBalance);
	if (t && _days >= 7) text.push('7日: '+t);
	t = profitSummary(lastWeek, initialBalance);
	if (t) text.push('上7日: '+t);
	t = profitSummary(month, initialBalance);
	if (t && _days>=30) text.push('30日: '+t);
	t = profitSummary(lastMonth, initialBalance);
	if (t) text.push('上30日: '+t);
	
	if (all) {
		var _days = Math.floor(all.profitTime / 86400);
		all.profitTime %= 86400;
		var _hours = Math.floor(all.profitTime / 3600);
		var drawback = _N( all.drawback*100/(all.drawbackProfit+initialBalance), 3 )+'%';
		text.push('总: 收'+_N(all.close,2)+'元('+_N(all.close*100/initialBalance,3)+'%)，最大回撤'+drawback+'，统计时间'+_days+'天'+_hours+'小时');
	}
	return text.join('\n');
};

function profitSummary(p, base) {
	if (!p) return '';
	var text = [];
	text.push('收'+_N(p.profit,2)+'元('+_N(p.profit*100/(base+p.open), 3)+'%)');
	var month = expectProfit(p, 30, base);
	if (month) {
		text.push('月化'+month.percent+'%');
	}
	var year = expectProfit(p, 365, base);
	if (year) {
		text.push('年化'+year.percent+'%');
	}
	text.push('回撤'+ _N( p.drawback*100/(p.drawbackProfit+base), 3 )+'%' );
	return text.join('，');
}


function expectProfit(p, days, base) {
	var expectSeconds = days*86400;
	if (expectSeconds < p.profitTime) return;
	return {
		profit: _N(p.profit * expectSeconds / p.profitTime, 2),
		percent: _N(p.profit * expectSeconds *100 / (p.profitTime * (base+p.open)),3)
	};
}

function main() {
    while(true) {
        var t = exchange.GetTicker();
        $.LogProfit(t.Last);
        LogStatus($.ProfitSummary(10000));
        Sleep(3600000);
    }
}
```

> Detail

https://www.fmz.com/strategy/19329

> Last Modified

2016-08-11 11:41:36
