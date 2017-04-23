---
layout: post
title:  前端开发中遇到的问题（JavaScript-jQuery篇）
date:   2017-04-23 23:03:00 +0800
categories: 前端之路
tag: 学习笔记
---

* content
{:toc}


### 写在前面的话
好记性不如烂笔头，开发中当中总会遇到各种各样的问题，有时候为了解决某些问题甚至是寻找答案很久，网上大牛的解答也是五花八门，有的能理解，有的不能理解，要一个一个去查看去分辨那些解答才是你想要的，无形当中又浪费了宝贵的时间。

而且随着时间的流逝遇到的问题多了，有的甚至会忘记当初是怎么解决的了，然后再次遇到的话还得再次去查找，也是很浪费时间。记录积累起来方便自己查看，同时也希望能有机会给他人一些参考，独乐乐不如众乐乐。

重要的一点是，回顾总结自己遇到的问题，是对自己知识的重新梳理，让知识在大脑里回炉一遍，变成自己的东西然后再输出，这对于自己成长是很有价值的事情。这才是最重要的。

所以，这是一篇主要写给自己的文章。同时也欢迎其他喜欢前端的朋友浏览，如果有人看了并且发现有不对的地方也欢迎提供宝贵的意见。

---------------------------------------------
### Javascript

###### 从URL中获取参数的方法
- 

```
//javascript
var urlParams;
function getUrlParam(key){
    if(!urlParams){
        //把当前显示文档的完整URL保存到变量URL中
        var url=location.href;
        //如果url中返回索引值 ? 第一次出现的调用的位置下标大于0进入下面函数
        if(url.indexOf('?')>0){
            //提取URL中介于？之后的字符串，然后从&符号处分割成两个字符串在一个数组里，赋值给变量paramsString
            var paramsString = url.substring(url.indexOf("?") + 1, url.length).split("&");
            var paramItem,i;
            // 创建一个空对象
            urlParams = {};
            // 遍历提取过的的参数字符串
            for (i = 0; i<paramsString.length; i++) {
                //把第每个字符串中从 = 处分割成两个字符串返回到一个数组
                paramItem = paramsString[i].split('=');
                //把返回paramItem数组中下标为1的值赋值给urlParams空对象下标为0的值
                urlParams[paramItem[0]]=paramItem[1];
            }
        }else{
            // 如果有URL参数返回空
            return "";
        }
    }
    if(key)return urlParams[key]||"";
    return urlParams;
}
获取的是url中?号后面的 key和value,
假如当前网址是https//:127.0.0.1:5000/index.html?Id=110&name=xiaoming
var Id = getUrlParam(Id); 
console.log(Id); //输出110
var name = getUrlParam(name); 
console.log(name); //输出xiaoming
```

###### 注册页面，密码输入框点击小眼睛切换密码显示与隐藏
 - 功能实现重点就是点击小眼睛改变input的type值和小眼睛图片img的src路径

```

//html
<li>
     ![](img/invisible.png)
     <input id="inputInVisible"  type="password"  placeholder="设置密码6-30位密码" maxlength="30"/>
</li>

//javascript
//页面加载执行
showPsw();
function showPsw() {
    //定义一个变量n
    var n =1;
      //点击小眼睛图片执行
    $("#visible").on('click', function() {
        当n取模不等于0切换input的type属性和img的src路径，然后n自增1，此时n=2
        if (n%2 != 0) {
            $('#inputInVisible').attr('type', 'text');
            $('#visible').attr('src', 'img/visible.png');
            n++;
        }else if (n%2 == 0){
//因为n=2，所以再次点击跳过一个条件，进入这个条件语句内，继续切换type的值和img的scr路径，然后n自减1，下次点击又执行上面条件内的语句，如此反复。
            $('#inputInVisible').attr('type', 'password');
            $('#visible').attr('src', 'img/invisible.png');
            n--;
        }
    });
}
```
（未完待续...）

