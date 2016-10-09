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


## 1. Field定义
```python
	real_name = models.CharField(max_length=100, null=True, verbose_name='...', help_test='...')
```

## 2. to_json
```python
	exclude_fields = {'create_time'}
	return {
		field.name: getattr(field.name) for field in MyModel._meta.get_fields() if field.name not in exclude_fields
	}
```
