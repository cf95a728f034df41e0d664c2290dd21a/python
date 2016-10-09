```python
# /home/capric/data/yqjr/Python/trunk/dcs/jd/utils.py@line 49

def getHobbies(hobbies):
	hobbiesStr=""
	for x in hobbies:
		if x == "1":
			hobbiesStr+= "图书/音像/数字商品"
		elif x == "2":
			hobbiesStr+= "家用电器"
		elif x == "3":
			hobbiesStr += "手机/数码"
		elif x == "4":
			hobbiesStr += "电脑/办公"
		elif x == "5":
			hobbiesStr += "家居/家具/家装/厨具"
		elif x == "6":
			hobbiesStr += "服饰内衣/珠宝首饰"
		elif x == "7":
			hobbiesStr += "个护化妆"
		elif x == "8":
			hobbiesStr += "鞋靴/箱包/钟表/奢侈品"
		elif x == "9":
			hobbiesStr += "运动健康"
		elif x == "10":
			hobbiesStr += "汽车用品"
		elif x == "11":
			hobbiesStr += "母婴/玩具乐器"
		elif x == "12":
			hobbiesStr += "食品饮料/保健食品"
		elif x == "13":
			hobbiesStr += "彩票/旅行/充值/票务"
		else:
			pass
	return hobbiesStr

```


```python
def get_hobbies(hobbies):
    branch = {
        "1": "图书/音像/数字商品",
        "2": "家用电器"
    }
    
	hobbies_str=""
	for h in hobbies:
        s = branch.get(h)
        if s:
            hobbies_str += s
            
    return hobbies_str

```
