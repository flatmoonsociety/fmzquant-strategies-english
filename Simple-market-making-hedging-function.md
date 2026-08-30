
> Name

Simple market making hedging function
> Author

3piggy

> Strategy Description

Small platforms make their own markets, reduce risks, and hedge with large exchanges
Strategic thinking:
An endless loop polls the account asset balance and hedges the changed coins to Huobi
Send DingTalk and WeChat notifications to the administrator at the same time
Use SQLite to save historical account balances and serve other strategies to facilitate financial management.


> Source (python)

``` python
# -*- coding: UTF-8 -*-
import time
from api import *
from Huobiapi import *
import sqlite3

def wechatmsg(text,desp):
	server = 'https://sc.ftqq.com/xxxxxx.send'
	payload = {'text':text,'desp':desp}
	requests.post(server,params = payload)

def dingmsg(title,msg):
	url = 'https://oapi.dingtalk.com/robot/send?access_token=xxxxxx'
	data = {
			 "msgtype": "markdown",
			 "markdown": {
				 "title":title+msg,
				 "text": "#### " + title + "\n"
						 "> " + msg						 
			}}		 
	header = {'Content-Type':'application/json'}
	r = requests.post(url = url ,headers=header,data = json.dumps(data)).json()
	return r

def check():
	try:
		pre_balance = {}
		conn = sqlite3.connect("/root/bot/hedge.db")
		cursor = conn.cursor()
		sql = 'select * from balance order by id desc limit 20;'
		result = list(cursor.execute(sql))
		for a in result:
			if a[1] in list(pre_balance.keys()):
				break
			else:
				pre_balance[a[1]] = a[2]   #读取之前balance
		coinname = list(pre_balance.keys())
		print(pre_balance,coinname)

		balance = GetBalance()
		t = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))
		for x in balance:  
			sql = "insert into balance (coin,balance,time) values(?,?,?);"
			b = x['balance']+x['frozenBalance']
			if b != 0:
				v = (x['coin']['unit'],b,t)
				print(v)
				cursor.execute(sql,v)
			for n in coinname:
				if n == x['coin']['unit']:
					d = round(b - pre_balance[n],5)   #数量差
					if d > 0:
                        Sell(n,d)
						msg = '对冲卖出'+n+'数量：'+str(d)
						print(msg)
						wechatmsg('对冲',msg)
						dingmsg('对冲',msg)
						sql = "insert into hedge (coin,hedge_amount,status,time) values(?,?,?,?);"
						v = (n,d,0,t)
						cursor.execute(sql,v)
					elif d < 0:
                        Buy(n,d)
						msg = '对冲买入：'+n+'数量：'+str(d)
						print(msg)
						wechatmsg('对冲',msg)
						dingmsg('对冲',msg)
						sql = "insert into hedge (coin,hedge_amount,status,time) values(?,?,?,?);"
						v = (n,d,0,t)
						cursor.execute(sql,v)
					else:
						print('no hedge')

		conn.commit()
		conn.close()
	except Exception as e:
		raise e
	
def insert_balance():
	try:
		conn = sqlite3.connect("hedge.db")
		cursor = conn.cursor()
		balance = GetBalance()
		t = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time()))
		for x in balance:
			sql = "insert into balance (coin,balance,time) values(?,?,?);"
			b = x['balance']+x['frozenBalance']
			if b != 0:
				v = (x['coin']['unit'],b,t)
				cursor.execute(sql,v)
		conn.commit()
		conn.close()
		print('finish')
	except Exception as e:
		print('err',e)

if __name__ == '__main__':
	while 1:
		try:
			check()
		except Exception as e:
			print(e)
		time.sleep(30)


```

> Detail

https://www.fmz.com/strategy/178194

> Last Modified

2019-12-12 14:39:05
