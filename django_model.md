```python
# /home/capric/data/yqjr/Python/trunk/dcs/jd/models.py@line 11
class UserInfos(models.Model):
	'''
	用户基本信息表描述
	real_name       真实姓名
	gender          性别
	email           邮箱
	birthday        出生日期
	marriage        婚姻状况
	month_salary    月薪
	idcard          身份证
	education       教育程度
	industry        所在行业
	qq              qq号
	username        用户名
	password        密码
	wechat          微信
	hobbies         爱好
	create_time     创建时间
	'''
	real_name=models.CharField(max_length=100,null=True)
	gender=models.CharField(max_length=10,null=True)
	email=models.CharField(max_length=50,null=True)
	birthday=models.CharField(max_length=50,null=True)
	marriage=models.CharField(max_length=10,null=True)
	month_salary=models.CharField(max_length=50,null=True)
	idcard=models.CharField(max_length=50,null=True)
	education=models.CharField(max_length=10,null=True)
	industry=models.CharField(max_length=30,null=True)
	qq=models.CharField(max_length=30,null=True)
	username=models.CharField(max_length=50,null=True)
	password=models.CharField(max_length=50,null=True)
	wechat=models.CharField(max_length=50,null=True)
	hobbies=models.CharField(max_length=500,null=True)

	create_time=models.DateTimeField(auto_now_add=True)

	class Meta:
		db_table = 'jd_user_infos'

	def to_json(self):
		return {

			'real_name': self.real_name,
			'gender': self.gender,
			'email': self.email,
			'birthday': self.birthday,
			'marriage': self.marriage,
			'month_salary': self.month_salary,
			'idcard': self.idcard,
			'education': self.education,
			'industry': self.industry,
			'qq': self.qq,
			'username': self.username,
			'password': self.password,
			'wechat': self.wechat,
			'hobbies': self.hobbies,

		}
```
