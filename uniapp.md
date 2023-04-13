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



###### 3. editor

>1. show-img-size:
>
>+ 点击图片时显示图片大小控件
>
>2. show-img-toolbar：
>
>+ 点击图片时显示工具栏控件
>
>3. show-img-resize
>
>+ 点击图片时显示修改尺寸控件
>
>4. @ready="onEditReady":(名字不可改)
>
>+ 编辑器初始化完成时触发引号内方法
>
>5. @focus="onFocus"(引号内部为方法，需要在methods内定义，名字不可改)
>
>+ 编辑器聚焦时触发引号内方法


>+ onEditReady具体定义
>
> ```uniapp
> onEditReady(){
> 	uni.createSelectorQuery().in(this).select('.myEdit').fields({
>         size:true,
>         context:true
>     },res=>{
>         console.log(res);
>         this.editorCtx=res.context
>     }).exec()
> }
> ```
> 

>+ this.editorCtx.format("name","value")
>
>1. name:富文本样式
>2. value：具体值，如果没有可不写
>3. 具体参数见[editorContext | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/api/media/editor-context.html#)

> + editorContext.insertImage({})
>
> 1. src：图片地址，仅支持 http(s)、base64、本地图片
> 2. alt：图像无法显示时的替代文本
> 3. 其他一些参数及插入函数见[editorContext | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/api/media/editor-context.html#)

>+ editorContext.getContents({})
>
>1. 获取富文本内容
>2. 具体参数及其他获取函数见[editorContext | uni-app官网 (dcloud.net.cn)](https://uniapp.dcloud.net.cn/api/media/editor-context.html#)





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



#### 1.3 VUE组件

##### 1.component

>1. 项目根目录下创建`components`目录，在目录内新建组件(scss模板，创建同级目录)
>2. 子组件传值：(value上的`“”`必须要)
>
>	```html
>	<componentName :var1="vlaue"></componentName>
>	```
>
>3. 父组件接受值：(位置在<script>根位置)
>
>	```JS
>	props:{
>	    var1:{
>	        type:typename
>	        default(){
>		
>	        }
>	    }
>	}
>	```
>
>4. 父组件使用值：跟正常html一样{{var1}}




### 2.API

#### 2.1 通用参数

>+ success/fail/complete
>
>```uniapp
>success: res=>{}
>```



#### 2.2 页面和路由

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



#### 2.4 媒体

##### 1.uni.chooseImage

>+ 返回参数为tempFiles(Object类型，具有属性name,path)



### 3.全局文件

#### 3.1 pages.json页面路由

##### 3.1.1 tabBar

>1. color：tab上的文字默认颜色
>2. selectedColor：tab 上的文字选中时的颜色
>3. backgroundColor：tab 的背景色
>4. list：
>
>+ pagePath：页面路径，必须在 pages 中先定义
>+ text：tab 上按钮文字
>+ iconPath：图片路径
>+ selectedIconPath：选中时的图片路径

##### 3.1.2 uniIDRouter

> ```JS
> "uniIdRouter": {
>     "loginPage": "pages/index/index", // 登录页面路径
>     "needLogin": [
>         "pages/detail/.*" // 需要登录才可访问的页面列表，可以使用正则语法
>     ],
>     "resToLogin": true // 自动解析云对象及clientDB的错误码，如果是客户端token不正确或token过期则自动跳转配置的登录页面，配置为false则关闭此行为，默认true
> }
> ```
>
> 



### 4.格式

#### 4.1 html

> 1. 初始化或更改值均使用=====
> 2. 在<view>等标签内，变量不为num类型时需要写在==“”==内
> 3. 在<view>等标签外，变量需要写在=={{}}==内



#### 4.2 JS

##### 1.格式问题

> 1. data(){},onload(){},methods{}(后面称这些为**不同区域**)等之间要使用==,==隔开
>
> 2. 不同区域间相互引用要使用==this.==隔开,template中则不需要使用
>
> 3. ==“”==嵌套使用则最外面的需要修改为==‘’==
>
> 4. 区域内部使用==,==或==;==隔开(==,==表示子句分隔，==;==表示语句终结)
>
> 5. 引入JS文件的函数：
>
> 	+ `import {funName} from "fileUrl"`
>
> 6. 区域内赋值的三种情况:
>
>    + **data中初定义** / **官方函数需要赋初值的参数(url等)**赋初值，使用==:==
>
>    + **函数内自己定义但之前未声明过的参数**赋初值，使用==let var1 = var2==
>
>    + 更改值(被更改的变量已经有初值)，使用=====
>
> 7. url/src:
>
>   + 相对路径(相对于当前文件所在文件夹位置)：==../==表示上一个文件夹(相对路径)
>
>   + 绝对路径:`"/uni_modules/uni-id-pages/pages/userinfo/userinfo"`//page.json时复制前方加上==/==
>
>   + 带参数:`/pages/detail/detail?cid=${e.classid}&id=${e.id}` //两端为==``==(反引号)

##### 2.正则表达式


>1. `?`:`?`前一个字符可以出现0次或1次，如`abc?`会匹配`ab`或`abc`
>2. `*`:`*`前一个字符可以出现0次、1次或多次，如`ab*c`会匹配`ac` `abc` `abbc`
>3. `+`:`+`前一个字符可以出现1次或多次，如`ab+c`会匹配`abc`或`abbc`
>4. `{}`:`{}`内可指定前一个字符出现的次数，次数后加`,`表示出现指定次数以上，如`ab{2}c`会匹配`abbc`
>5. `()`:搭配前面的限定符可以指定字符串，如`(ab)+c`会匹配`ababc`
>6. `(|)`:或运算，如`(a|b)c`会匹配`ac`或`bc`
>7. `[]`:`[]`内包含字符集，会匹配字符集内的字符，`[^a-zA-Z0-9]`表示所有非大小写字母及0-9数字的字符
>8. `^a a$`:`^a`只会匹配行首的`a`，`a$`只会匹配行尾的`a`
>9. `\b`:表示单词字符边界，如`ab\b`会匹配`abab`后面的`ab`
>10. `.`:表示任意字符
>11. `元字符`:`\d`表示数字字符，`\w`表示所有英文数字下划线，`\s`表示空白符(`\`后换成大写字母表示非)
>12. `转义`:`\`加上限定符表示限定符本身，如`\+`会匹配`+`



#### 4.3 VUE

>1. v-bind: 缩写==:==,在绑定prop或者用变量动态赋值时需要使用
>
>2. v-model：v-model=“data”,对表单和数据进行双向绑定，表单不需要提交即可更改数据，`v-model.`后可以接类型
>3. v-for: 需要绑定使用==:key==；v-for=“(item,index) in List”,此时index为数组序号





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

##### 8.云端环境变量

> 1. $cloudEnv_uid:当前用户uid，依赖uni-id
> 2. $cloudEnv_now:服务器时间戳
> 3. $cloudEnv_clientIP:当前客户端IP



#### 2.3 unicloud-db组件

##### 1.基本格式

> ```html
> <unicloud-db v-slot:default="{data, loading, error, options}" 
>  collection="database" field="field1" :getone="true" where="id=='1'">
>     <view v-if="error">{{error.message}}</view>
>     <view v-else-if="loading">数据加载中</view>
>     <view v-else>{{data}}</view>
> </unicloud-db>
> ```

##### 2.联表查询

> ```html
> //var1为database1里的属性，var2为database里的属性
> <unicloud-db v-slot:default="{data, loading, error, options}"
>  collection="database1,database2" field="var1,FK.var2"></unicloud-db>
> ```

##### 3.loadtime

>
>
>





### 3.云存储

#### 3.1 uploadFile

> + uploadFile({Object})
> + Object属性：
> 	1. filePath：上传的文件地址
> 	2. cloudPath：云端文件名
>
> + 返回属性：FileID，用于访问文件，建议储存



#### 3.2 uni-file-picker

> + 更多参数见[uni-file-picker文档](https://uniapp.dcloud.net.cn/component/uniui/uni-file-picker.html#)

> ```html
> <uni-file-picker 
> 	v-model="imageValue" 
> 	fileMediatype="image" //限制上传类型
>        :limit="1"	//上传数量
> 	mode="grid" 
>        ref="files"	//通过ref调用upload方法自行选择上传时机
>  	:auto-upload="false"	//关闭自动上传
> 	@select="select" //这些函数不需要可以不写，否则会报错
> 	@progress="progress" 
> 	@success="success" 
> 	@fail="fail" 
> />
> <button @click="clickUpload">上传文件</button>
> <script>
> 	export default {
> 		data() {
> 			return {
> 				imageValue:[]
> 			}
> 		},
> 		methods:{
>             //上传文件
>             clickUpload(){
>                 this.$refs.files.upload()
>             }
> 			// 获取上传状态
> 			select(e){
> 				console.log('选择文件：',e)
> 			},
> 			// 获取上传进度
> 			progress(e){
> 				console.log('上传进度：',e)
> 			},
> 			
> 			// 上传成功
> 			success(e){
> 				console.log('上传成功')
> 			},
> 			
> 			// 上传失败
> 			fail(e){
> 				console.log('上传失败：',e)
> 			}
> 		}
> 	}
> </script>
> 
> ```



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



#### 4.3 用户登录

>1. 引入store.js
>
>	```JS
>	import {
>	store,
>	mutations
>	} from '@/uni_modules/uni-id-pages/common/store.js'
>	```
>
>2. 添加computed属性
>
>	```JS
>	computed:{
>	    userInfo() {
>	        return store.userInfo
>	    },
>	    hasLogin(){
>	        return store.hasLogin
>	    }
>	}
>	```
>
>	3. 配置uniIDRouter

#### 4.4 用户登出

>1. 引入store.js就调用
>
>	```JS
>	import {mutations} from "@/uni_modules/uni-id-pages/common/store.js"
>	mutations.logout() //调用logout函数
>	```
>
>2. 修改(按情况，本项目需要)
>
>	+ logout函数
>
>	```JS
>	uni.redirectTo({
>	    url: `/${pagesJson.uniIdRouter?.loginPage ?? 'pages/self/self'}`,
>	});
>	```
>	
>	+ updateUserInfo函数
>	
>	```JS
>	let res = await usersTable.where("'_id' == $cloudEnv_uid")			.field('mobile,nickname,username,email,avatar_file,register_date')
>	.get()
>	```
>	
>	
>
>
>

#### 4.5 多端角色管理

>1. 在uniCloud/cloudfunctions/common/uni-config-center/uni-id路径下创建hooks/index.js
>
>2. 修改index.js内容为
>
>	```JS
>	// 钩子函数示例 hooks/index.js
>									
>	function beforeRegister({
>	  userRecord,
>	  clientInfo
>	} = {}) {
>	  if(clientInfo.appId === 'AppID') {	//manifest.json中可查看
>	    if(userRecord.role) {
>	      userRecord.role.push('roleName')	//在uni-admin中创建
>	    } else {
>	      userRecord.role = ['roleName']
>	    }
>	  }
>	  return userRecord // 务必返回处理后的userRecord
>	}
>									
>	module.exports = {
>	  beforeRegister
>	}
>	```
>
>	



### 5.uni-admin

>1. 新建项目，选择模板uni-admin，并关联云服务空间
>2. 右键选择关联云服务空间，并点击绑定其他项目的服务空间
>3. 右键选择移动至关联云服务空间



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



#### 1.5 修改层级

> ```css
> z-index: 100;	//显示在最上层
> ```



#### 1.6 点击显示样式

>```css
>&.active{	//CSS写好点击后的样式
>    color:#FB7299
>}
>```
>
>```html
>:class="condition ? 'active' : ''"
>//在标签使用上述表达式并添加点击事件，在点击事件内修改condition
>```

#### 1.7 背景高斯模糊

> ```CSS
> position: absolute;
> top: 0;
> left:0;
> width: 100%;
> height: 100%;
> overflow: hidden;
> image{
>     width: 100%;
>     height: 100%;
>     filter: blur(20px);
>     transform: scale(2);
>     opacity: 0.5;
> }
> ```



#### 1.8 盒子接触部分两端圆角

>```css
>border-radius: 30rpx;
>transform:translateY(-30rpx);//参数与border-radius的参数保持一致
>```



#### 1.9 iconfont字体库

>1. [iconfont官网](https://www.iconfont.cn/)找到我的项目并下载解压，留下iconfont文件(除后缀名为json)
>2. 在App.vue文件<style>中添加`@import "@/static/fonts/iconfont.css"`
>3. 修改iconfont.css文件最上方的url，添加`@/static/fonts/`
>4. 在需要的地方使用`class="iconfont iconname"`(修改样式时用`.iconfont{font-size=50rpx}`)



### 2.常见问题

#### 2.1 图像类

##### 1.图像显示溢出/盒子边界

> + 图像显示溢出/盒子边界
>
> ```css
> image{
>     width:100%;
>     height:100%;
>     box-sizing: border-box;//可写在全局
> }
> ```

##### 2.系统状态栏压住盒子

> ```CSS
> padding-top:var(--status-bar-height);
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
