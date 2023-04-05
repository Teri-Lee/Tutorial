# 微信小程序

## 一.uniapp

### 1.组件

#### 1.1 表单组件

##### 1.1.1 基础

>```html
><form @submit="onSubmit"></form>	//提交表单
>```
>
>```script
>onSubmit(e){...}		//提交函数(注意e为提交的内容)
>```
>

##### 1.1.2相关组件

###### 1. button


>1. form-type:
>
>+ reset:点击重置
>+ submit:点击提交(常搭配1.1)
>
>2. size:
>
>+ default:常规大小
>+ mini:小尺寸
>
>3. type:
>
>+ primary:不同平台不同颜色
>+ default:白色
>+ warn:红色



###### 2. input

>1. type:
>
>+ text/number/digit:文本/数字/带小数数字
>+ idcard/tel/safe-password：身份证/电话/安全密码输入键盘
>
>2. name：
>
>+ 提交后的名称(必填)
>
>3. placeholder
>
>+ 预输入内容

#### 1.2 媒体组件

##### 1.image

> 1. src:
>
> + 具体格式见本章3.2.6
>
> 2. mode:
>
> + aspectfill:保持短边缩放，裁剪长边
>+ aspectFit:保持长边缩放，无裁剪



### 2.API

#### 2.1 通用参数

>+ success/fail/complete
>
>```uniapp
>uccess: res=>{}
>```



#### 2.2 路由

> **1. uni.navigateTo**:保留当前页，跳转到其他页面，可返回
> **2. uni.redirectTo**:关闭当前页，跳转到其他页面，不可返回
> **3. uni.relaunch**:关闭所有页，跳转到其他页面，不可返回

>1. url(此为上面三个API通用参数)：
>
>+ 具体格式见本章3.2.6



#### 2.3 交互

##### 1.uni.showToast

>+ title:显示文本
>+ icon:图标(success/error/fail/exception/loading/none(不显示))
>+ mask:是否防止触摸穿透
>+ duration:持续时间，单位毫秒

> + 捕捉异常
>
> ```uniapp
> Fun(){}.then(res=>{
> 	uni.showToast({			//调用成功
> 		icon:"success"
> 	})
> }).catch(err=>{
> 	uni.showToast({			//捕获失败
> 		title:err.message,
> 		icon:"none"
> 	})
> })
> ```

##### 2.uni.hideToast

> + 隐藏消息提示框





### 3.格式

#### 3.1 html

> 1. 初始化或更改值均使用=====
> 2. 在<view>等标签内，变量不为num类型时需要写在==“”==内
> 3. 在<view>等标签外，变量需要写在=={{}}==内
> 4. v-for需要绑定使用==:key==



#### 3.2 JS

> 1. data(){},onload(){},methods{}(后面称这些为**不同区域**)等之间要使用==,==隔开
> 2. 不同区域间相互引用要使用==this.==隔开,template中则不需要使用
> 3. ==“”==嵌套使用则最外面的需要修改为==‘’==
> 4. 区域内部使用==,==或==;==隔开(==,==表示子句分隔，==;==表示语句终结)
> 5. 区域内赋值的三种情况:
>
>    5.1 **data中初定义** / **官方函数需要赋初值的参数(url等)**赋初值，使用==:==
>
>    5.2 **函数内自己定义但之前未声明过的参数**赋初值，使用==let var1 = var2==
>
>    5.3 更改值(被更改的变量已经有初值)，使用=====
>
> 6. url/src:
>
> 	6.1 相对路径(相对于当前文件所在文件夹位置)：==../==表示上一个文件夹(相对路径)
>
> 	6.2 绝对路径:"/uni_modules/uni-id-pages/pages/userinfo/userinfo"//page.json时复制前方加上==/==
>
> 	6.3 带参数:`/pages/detail/detail?cid=${e.classid}&id=${e.id}` //两端为==``==(反引号)



3.3 VUE

>1. v-bind:缩写==:==,在绑定prop或者用变量动态赋值时需要使用
>
>

## 二.uniCloud

### 1.云函数/云对象

#### 1.1 云对象

##### 1.创建云对象

>```uniCloud
>const db=uniCloud.database();	//连接数据库
>module.exports = {
>	_before: function () { // 通用预处理器
>
>	},
>	async Fun1(num){		//常规方法定义函数(类似云函数)
>		return await db.collection("database").get();
>	}，
>	Fun2:async()=>{		//箭头函数方法定义函数
>		await db.collection("database").get()
>	}
>}
>```

##### 2.调用云对象

> ```uniCLoud
> const cloudObj=uniCloud.importObject("cloudObj")//定义在script内最外层
> cloudObj.Fun().then(res=>{...})		//调用云对象内具体函数(同云函数)
> ```



#### 1.2 云函数

##### 1.2.1创建云函数

> ```uniCloud
>const db=uniCloud.database();
> exports.main = async (event, context) => {
> 	return await db.collection("database").get();
> };
> ```
> 

##### 1.2.2调用云函数

> ```uniCloud
> uniCloud.callFunction({
>    name:"Fun_name",		//后端定义的函数名
>    data:{				//传到API的数据，一般为对象
>         detail:detail	//当属性和值相等时，可简写为detail
>    }
> }).then(res=>{
>    console.log(res)
> })
> ```



### 2.云数据库

#### 2.1 DB Schema

##### 2.1.1 required

> ```DB Schema
> "required": ["keyword"] //必填字段，常搭配2.1.3 中的errorMessage
> ```

##### 2.1.2 permission

> + 前端非admin权限，默认为false
> + “auth.uid!=null”  //只有登录才有权限
> + “doc.userId==auth.uid”  //操作对应的表与操作用户为同一人

##### 2.1.3 properties

>+ **“bsonType”**:字段类型
>
>+ **“title”**:标题
>
>+ **“discription”**:描述
>
>+ **“errorMessage”**:错误信息(常搭配2.1.1 required)
>
>+ **“trim”:**去除空白字符(仅对string有效)
>
>	​	1.none:不去除(默认)
>
>	​	2.both/start/end:去除位置
>
>+ **”defaultValue”(非强制)/“forceDefaultValue”(强制)**:默认值，下面列举几个特殊**对象**默认值
>
>	​	1.timestamp：{“$env”:”now”}	//时间戳
>	
>	​	2.userId：{“$env”:”uid”}	//userId可换成其他名字,属性为string



#### 2.2 JQL

##### 1.添加

> ```JQL
>let {object}=event;   //前端读取的数据,多条数据用,隔开
> 
> return await db.collection("database").add({	//内接对象{}
>   posttime:Date.now(),
>   ...object	//对象解构为一条一条的属性，搭配{}增加其他属性并重构对象
>    })
>    ```
> 

##### 2.修改

> ```JQL
> db.collection("database").doc("_id").update({var:value})	//doc一般接唯一标识符"_id
> db.collection("database").where("age>25 && age<40").update({arr: {1: "uniCloud"}})
> //数组可直接使用下标
> ```

##### 3.删除

> ```JQL
> db.collection("database").doc("_id").remove()
> db.collection("database").where('name=="Lee"').remove()
> ```

##### 4.联表查询

> ```JQL
> //联表查询一定要在第一张表内设置foreignKey
> 
> //缩略写法(不要求长期存在可用let代替const)
> const database1=db.collection('database1').where('_id=="1"').getTemp() //第一张表按FK查询
> const res=await db.collection(database1,'database2').get()	//联表查询
> 
> //完整写法(获取所求表所有内容再拼接，由于权限问题往往需要字段过滤)
> const database1=db.collection('database1').getTemp()
> const database2=db.collection('database2').getTemp()
> db.collection(database1,database2).get().then(res=>{...})
> ```

##### 5.字段过滤

> ```JQL
> //foreignKey在不同表名称不一样，建议参考Schema
> const database1=db.collection('database1').filed("FK,var1...").getTemp()
> const database2=db.collection('database2').field("Fk,var2...").getTemp()
> db.collection(database1,database2).get().then(res=>{...})
> 
> //别名，之后渲染都使用别名varname
> const database1=db.collection('database1').filed("FK,var1 as varname...").getTemp()
> ```
>

##### 6.排序

>```JQL
>//按照quantity字段升序排序，quantity相同时按照create_date降序排序
>.orderBy('quantity asc, create_date desc')
>```

##### 7.限制查询条数

> ```JQL
> .limit(num)//limit限制一条或多条记录，结果为对象组成的数组，
> .get({getone:true})//getone只查询一条记录，结果为对象
> ```





### 3.云存储



### 4.uni-id

#### 4.1 初始配置

> 1. 前往[uni-id-pages - DCloud 插件市场](https://ext.dcloud.net.cn/plugin?name=uni-id-pages)导入插件
>
> 2. 在uniCloud/cloudfunctions/common/uni-config-center路径下创建uni-id/config.json
> 3. 前往[uni-id云端配置说明](https://uniapp.dcloud.net.cn/uniCloud/uni-id-summary.html#config)复制config.json
> 4. 删除config.json中的注释(替换-正则匹配-==//.+==-全部替换)
> 5. 配置config.json:
>
> + “passwordSecret”:用于加密密码入库的密钥,要求长字符串(此项需手动添加)
> + “tokenSecret”:生成token需要的密钥,要求长字符串

#### 4.2 数据库绑定

>```JS
>"userId":{		//在表的properties下添加该字段
>    "bsonType": "string",
>    "title": "用户Id",
>    "foreignKey": "uni-id-users._id",
>    "defaultValue":{
>        "$env": "uid"
>    }
>}
>```

#### 4.3 用户登出

> ```JS
> import {mutations} from "../../uni_modules/uni-id-pages/common/store.js"
> //引入JS文件，logout函数就在这个文件里
> mutations.logout()
> //调用logout函数；如果想要修改logout函数(如注销后的登录界面)，去store.js修改
> ```

#### 4.4 权限更改

>
>
>



## 三.CSS

### 1.特殊样式

#### 1.1 超出两行省略

> ```css
> text-overflow: -o-ellipsis-lastline;
> overflow: hidden;				//溢出内容隐藏
> text-overflow: ellipsis;		//文本溢出部分用省略号表示
> display: -webkit-box;			//特别显示模式
> -webkit-line-clamp: 2;			//行数
> //line-clamp: 2;					
> -webkit-box-orient: vertical;	//盒子中内容竖直排列
> ```



#### 1.2 弹性盒模型

>+ 左右(默认)/上下、紧贴(默认)/两端
>
> ```css
> display: flex;		//默认横向
> flex-direction: column;			//排列方向纵向
> justify-content: space-between;	//控制在方向两端(区分padding)
> ```

> + 居中
>
> ```css
> display: flex;
> justify-content: center;	//左右居中
> align-items: center;		//上下居中
> ```



#### 1.3 控制盒子相对位置

> ```css
> position: fixed;	//开启相对位置
> right: 60rpx;		//距离右侧相对位置
> bottom: 100rpx;		//距离底部相对位置
> ```
>



#### 1.4 边界(border)

> ```css
> border-bottom: 1rpx solid #eee;	//下划线
> border: 1rpx solid #eee 		//边界线
> ```



### 2.常见问题

#### 2.1 图像类

> + 图像显示溢出/盒子边界
>
> ```css
> image{
>     width:100%;
>     height:100%;
>     box-sizing: border-box;//可写在全局
> }
> ```



#### 2.2 格式类

> + 非view_class写格式不需要==.==
>
> ```css
> text{}、input{}、textarea{}等
> ```

> + 全局格式(写在app.vue)
>
> ```css
> *{
>     box-sizing: border-box;
> }
> ```
