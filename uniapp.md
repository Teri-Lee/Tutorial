# 微信小程序

## 一.uniapp

### 1.组件

+ 媒体组件

> **1.image**
>
> 1. src:
>
> + ==../==表示上一个文件夹(相对路径)
>
> 2. mode:
>
> + aspectfill:保持短边缩放，裁剪长边
> + aspectFit:保持长边缩放，无裁剪



### 2.API

+ 路由

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
> success: function(res) {}
> ```
>

## 二.uniCloud



## 三.CSS

### 1.特殊样式

+ 超出两行省略

> ```css
> text-overflow: -o-ellipsis-lastline;
> overflow: hidden;				//溢出内容隐藏
> text-overflow: ellipsis;		//文本溢出部分用省略号表示
> display: -webkit-box;			//特别显示模式
> -webkit-line-clamp: 2;			//行数
> //line-clamp: 2;					
> -webkit-box-orient: vertical;	//盒子中内容竖直排列
> ```



+ 弹性盒模型

>+ 左右(默认)/上下、紧贴(默认)/两端
>
> ```css
> display: flex;		//默认横向
> flex-direction: column;			//纵向
> justify-content: space-between;	//控制在方向两端(区分padding)
> ```

> + 居中
>
> ```css
> display: flex;
> justify-content: center;	//上下居中
> align-items: center;		//左右居中
> ```



+ 控制盒子相对位置

> ```css
> position: fixed;	//开启相对位置
> right: 60rpx;		//距离右侧相对位置
> bottom: 100rpx;		//距离底部相对位置
> ```
>
> 

### 2.常见问题

+ 图像类

> + 图像显示溢出
>
> ```css
> image{
>     width:100%
>     height:100%
> }
> ```



