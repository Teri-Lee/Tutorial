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



#### 1.2 媒体组件

##### 1.image

> 1. src:
>
> + ==../==表示上一个文件夹(相对路径)
>
> 2. mode:
>
> + aspectfill:保持短边缩放，裁剪长边
>+ aspectFit:保持长边缩放，无裁剪



### 2.API

#### 2.1 路由

> **1. uni.navigateTo**:保留当前页，跳转到其他页面，可返回
> **2. uni.redirectTo**:关闭当前页，跳转到其他页面，不可返回
> **3. uni.relaunch**:关闭所有页，跳转到其他页面，不可返回
>
> 1. url:
>
> ```uniapp
> url:`/pages/detail/detail?var1=${value1}&var2=${value2}`
> ```
>
> 2. success/fail/complete
>
> ```uniapp
> success: res=>{}
> ```
>



### 3.格式

#### 3.1 template

> 1. 初始化或更改值均使用=====
> 2. 在<view>等标签内，变量不为num类型时需要写在==“”==内
> 3. 在<view>等标签外，变量需要写在=={{}}==内
> 4. v-for需要绑定使用==:key==



#### 3.2 script

> 1. data(){},onload(){},methods{}(后面称这些为**不同区域**)等之间要使用==,==隔开
>
> 2. 不同区域间相互引用要使用==this.==隔开,template中则不需要使用
>
> 3. 区域内部可使用==,==或==;==隔开
>
> 4. 区域内赋值的三种情况:
>
> 	4.1 **data中初定义** / **官方函数需要赋初值的参数(url等)**赋初值，使用==:==
>
> 	4.2 **函数内自己定义但之前未声明过的参数**赋初值，使用==let var1 = var2==
>
> 	4.3 更改值(被更改的变量已经有初值)，使用=====



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

##### 1.2.3数据库操作

###### 1.数据库添加

> ```uniCloud
>let {object}=event;   //前端读取的数据,多条数据用,隔开
> 
> return await db.collection("database").add({	//内接对象{}
>   posttime:Date.now(),
>   ...object	//对象解构为一条一条的属性，搭配{}增加其他属性并重构对象
>    })
>    ```
> 



### 2.云存储





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
