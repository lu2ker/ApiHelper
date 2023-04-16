# ApiHelper

## 简介

这是一款依赖于BurpSuite中HTTP history的API测试辅助工具，能够帮助你分析单个站点的请求路径，快速从Json格式的响应数据中获取参数，便于进行FUZZ

## 菜单功能：

-   Send HttpContext
    -   在一个完整的请求中右键，选择Send HttpContext即可将当前数据包中Host主机的所有HTTP history发送到插件面板中；
    -   自动获取该Host的所有**响应体**中的Json数据，按键值对生成多行形如`a=b`的数据，同时还会**自动给键设置6位随机值**，便于FUZZ时的对比，将生成的结果去重后放置在AllParams标签内。
    -   自动获取该Host的所有请求路径，去重后放置在ReqPath标签内。
-   Get Json2Param(Response)
    -   对选中的单个或多个请求记录获取其**响应体**中的Json并转换为 键=值 的结果，**不自动设置随机值**，去重后放置在Result标签中。
    -   **只对Response进行处理**
-   Get Json2Param(Request)
    -   **只对Request进行处理**
    -   使用场景，Intruder跑完，对成功结果中的请求参数的提取。不过暂时还不能指定获取哪个参数，默认全部获取。

## 面板功能：

首先肯定是先要使用Send HttpContext发数据过来的。

视图：

<img width="1512" alt="image-20230416181200308" src="https://user-images.githubusercontent.com/68197734/232294524-44e58f06-2548-479a-ac95-f04937dd4615.png">


-   Filter
    -   输入Java支持的正则，点击按钮或者回车都可以。
    -   使用示例1: `/api/getUserList` 即可过滤`包含/api/getUserList`的请求。
    -   使用示例2: `getUserList|getRoles `即可过滤`包含getUserList`或者`getRoles`的请求。
    -   使用示例3: `admin.xxx.com && getUser`即可过滤`host为admin.xxx.com的包含getUser`的请求。
    -   **注意1：只可过滤：#、host、Method、url、statusCode表格内的字段值,不能根据包内容过滤。**
    -   **注意2：这里用到的逻辑与是` [space]&&[space]`，是包含空格的两个&；逻辑或是不包含空格的一个`|`**
-   Result、AllParams、ReqPath文本框
    -   Result: 主要放置处理结果的框；两个Get 菜单的结果也在这里；可以随着选择面板中的一行实时变化。
    -   AllParams: 随着面板中的过滤结果变化，初始是`Send HttpContext`的全部。
    -   ReqPath: 随着面板中的过滤结果变化，初始是`Send HttpContext`的全部。
-   Copy
    -   解放CV键，点一下即可复制当前文本框中的数据。
    
## 参考

-   https://github.com/pmiaowu/BurpFastJsonScan
-   https://github.com/c0ny1/captcha-killer

## 其他：

代码如屎山，故不开源~~自欺欺人~~

![image](https://user-images.githubusercontent.com/68197734/232294750-d0d10694-d70f-4f8b-a9a8-92ba8b874ab8.png)
