>本来没想过fork该代码，因为本来没有很多时间修修改改，感觉用着还好。但是越来越多不满意的地方，特别今天莫名其妙`tomcat`挂了，看了看日志根据前面报错，初步怀疑是首页加载太慢(第一次加载需要 30s 左右完成)，而用户直接退出去，导致服务器还在向浏览器发送数据(后面详说)。所以没办法了只能慢慢改进，毕竟体验有点差。
### 前言
欢迎体验我的个人博客 **一亩三分自留地**  [http://guozh.net](http://guozh.net)
### 改造过程
这里记录该博客的一些“私人定制”过程，有相同需求的可以借鉴一二
##### 1、点击网站logo期望跳转到首页
可能大家发现了，点击网站logo，只是重新请求了该网页地址，不太符合我自己的使用习惯，一般我喜欢点击后跳转到首页，如下图
![](http://images.bixiaode.com/dream/180731/DH5DcDJAl1.png?imageslim)
修改代码位置`header.html`
<br>
![](http://images.bixiaode.com/dream/180731/i5Gf1201cd.png?imageslim)
##### 2、浏览量不改变
以前在issues中提到过，直接戳[浏览量不更新没变化](https://github.com/ZHENFENG13/My-Blog/commit/528af45a56c3d6d06fdccecc1789e776c9710991)
##### 3、图片显示不全
![点击放大](http://images.bixiaode.com/dream/180731/k4GFIIeeLC.png?imageslim)
<br>
明显可以看出来，我自己的图片在显示不全，我仔细对比看了下代码
<br>
![mark](http://images.bixiaode.com/dream/180731/DCcGBikfaB.png?imageslim)
<br>
其实图片从长宽的 50% 开始显示。所以直接将这行去掉即可。找到
<br>
![mark](http://images.bixiaode.com/dream/180731/Lea9KecC3b.png?imageslim)
<br>
用记事本打开，查找到相应关键字`.item-thumb`，注意别找错了是下面这行
```
.item-thumb{position:relative;display:inherit;min-height:250px;background-position:50% 50%;background-size:cover}
```
去掉`background-position:50% 50%;`，保存修改完记得清除浏览器缓存
##### 4、第一次访问非常慢

