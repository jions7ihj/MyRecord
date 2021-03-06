>   简单解释什么是cookie，以及带来的一些问题
>   意外发现这方面的内容好多，蛮感兴趣的，以后有机会深入挖掘下隐私相关的问题

## 什么是cookie

>   Cookie（复数形态Cookies），中文名称为“小型文字档案”或“小甜饼”，指某些网站为了辨别用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。定义于RFC2109。是网景公司的前雇员卢·蒙特利在1993年3月的发明。
>
>   Cookie总是保存在客户端中，按在客户端中的存储位置，可分为内存Cookie(随浏览器关闭而消失)和硬盘Cookie。

## 用途

因为HTTP协议是**无状态**的，即服务器不知道用户上一次做了什么，这严重阻碍了交互式Web应用程序的实现。在典型的网上购物场景中，用户浏览了几个页面，买了一盒饼干和两饮料。最后结帐时，由于HTTP的无状态性，不通过额外的手段，服务器并不知道用户到底买了什么。 所以Cookie就是用来绕开HTTP的无状态性的“额外手段”之一。服务器可以设置或读取Cookies中包含信息，借此维护用户跟服务器会话中的状态。

Cookie另一个典型的应用是当登录一个网站时，网站往往会请求用户输入用户名和密码，并且用户可以勾选“下次自动登录”。如果勾选了，那么下次访问同一网站时，用户会发现没输入用户名和密码就已经登录了。这正是因为前一次登录时，服务器发送了包含登录凭据（用户名加密码的某种加密形式）的Cookie到用户的硬盘上。第二次登录时，（如果该Cookie尚未到期）浏览器会发送该Cookie，服务器验证凭据，于是不必输入用户名和密码就让用户登录了。

如果在一台计算机中安装多个浏览器，每个浏览器都会以独立的空间存放Cookie。因为Cookie中不但可以确认用户信息，还能包含计算机和浏览器的信息。

## Cookie的缺陷

1.  Cookie会被附加在每个HTTP请求中，所以无形中增加了流量。
2.  由于在HTTP请求中的Cookie是明文传递的，所以安全性成问题。（除非用[HTTPS](https://zh.wikipedia.org/wiki/HTTPS)）
3.  Cookie的大小限制在4KB左右。对于复杂的存储需求来说是不够用的。

## 关于隐私

首先说明：**浏览器对于各个网站的Cookies是隔离开的,不允许跨域访问**

Cookie和网站安全性设计的前提都是：**浏览器是安全的**，是不会偷窥用户私密数据的。如果浏览器存在漏洞，就可能给黑客可乘之机，获取cookie文件。另外浏览器主观伪造、利用用户cookie，在技术上也是可行的。

至于Cookies导致的隐私问题可能有以下几种

1.  精准投放广告会在其他网站上显示出曾经搜索过的关键词的相关广告。 如果恰巧有人与你共用电脑， 并且对方了解关键词与广告投放的关系。 那么他就能大致推断出你搜索了什么内容。


2.  Cookies对本地软件是不设防的。Cookies存放的位置一般是固定的。那么如果有流氓软件，你的Cookies内容(隐私)就可能会被这些软件搜集到。


3.  如果你访问的网站安全性存在一定问题，那么黑客可以通过XSS之类的攻击手段获取到该网站的Cookies内容，以达到Session劫持(无需账户密码即可登录你的帐号)之类的目的。(主要针对的一般是管理员，普通用户不用太担心这个)
4.  Cookies的确能记录你的很多个人信息，比如你经常访问哪类网页，在网页上停留多久，通常在什么时候上网等等。这些信息有些人可能毫不在乎，但如果有广告商集中搜集过去，就能掌握这个人的上网兴趣口味，有时还能推算出收入水平等个人信息。不过，对于很多地方强调的Cookies会保存用户密码问题，在我看来倒未必是迫在眉睫的危险，因为这些密码通常会用不可逆的方式加密，泄露出去也无法还原出用户密码；这方面可以说的东西很多

关于广告，这里说下，举个例子百度广告平台有很多广告商家投放广告，你搜索某个关键词被写入cookie，当你打开某个其他网站时，里面恰好有百度的广告位，那么就会读取之前保存的cookie发送到百度的广告平台，进行一系列算法优化处理，返回认为你所感兴趣的广告(根据你搜索的关键词等)，这也许就是所谓的被跟踪了

Google、网易等网站也通过这种方式来分析用户行为习惯，针对性地推送广告，并计算广告的投放效率。因此，像Google、百度、网易新浪这些超大型网站，拥有数亿甚至十几亿用户的Cookies都很正常，**只要不向第三方出售这些数据，目前他们拥有这些数据还是合法的**。（如果你是一个大老爷们不会想看到卫生XX的广告是吧？）

## 关于网络臭虫

首先你先要了解一些知识：

>   根据cookie的规范，只能把这些保存用户信息的小文件发给最初生成它们的域。那还怎么利用cookie跟踪我对其他网站的访问呢？
>
>   要知道答案，就得明白链接的工作原理。每个网页都包含指向其他页面的链接（这正是“超链接”的本义）。我们都知道链接必须由我们主动点击，然后浏览器才会打开或转向新页面。但图片不需要任何人点击，它会随着页面加载而自动下载。网页中引用的图片可以来自任何域。于是，在浏览器取得图片时，提供该图片的域就知道我访问过哪个页面了。而且这个域也可以在我的计算机上存放cookie，并且收到之前访问过的域所产生的cookie。

**网络臭虫的工作原理和惯用伎俩：**
在受用户欢迎、被广泛访问的网页上放置一个一像素大小的图片，这样用户看不到这张图片，但它依然可以正常工 作：它的工作就是通过获取Cookies来获知用户的浏览习惯。举例来说，现在窃贼公司在网易女人频道的所有网页上都放置了臭虫。当用户访问网易女人频道 页面时，**由于臭虫位于本网页，因此它有权下发、获得用户的Cookies(自己下发的)；又由于臭虫中内嵌了窃贼网站的地址，因此它可以把网易女人频道访问者的 Cookies搜集并回传到窃贼公司**。如果网易女人频道一天有1000万人访问，则该公司一天就获取了1000万份个人信息。但是这样大网站一般不会同意加入第三方的代码

关于上面的补充：如果想直接获得用户的cookies，那第三方广告如果直接就在网易的域名下，那真的可以做到的，但是如果在所谓“窃贼网站”的域名下，就很困难（cookies是彼此隔离的）。当然也不敢排除利用浏览器漏洞或者**Flash插件漏洞**来做。所以，在网页里看到第三方广告，不用太担心这些广告可以轻易拿走你的Cookie。一般都拿不到。除非这些第三方广告自己给你种Cookie，捕获你的行为。但我觉得，一般这又是门户广告商自己的蛋糕，一般会严格禁止广告投放商干这种事情。

## 预防

首先换个可信任的浏览器吧，比如chrome、firefox啦，然后保证更新你的flash，flash漏洞很可观；虽然现在google即将淘汰flash采用H5但是还是有大批网站在使用。

使用广告过滤插件如ADB之类可以屏蔽一些臭虫，虽然NoScript确实可以阻止cookies的窃取，但是.....太尼玛不方便了

记得最好开启浏览器的“发送不跟踪”请求

不过听说，像google、apple、microsoft这些巨头早就抛弃了cookies跟踪用户的方法，他们有更先进的技术 = =！

## 参考

https://www.kancloud.cn/kancloud/http-cookies-explained/48333

Cookie如何暴露你在互联网上的行踪：

http://www.guokr.com/blog/440916/

互联网风云之Cookie之争：

​https://zhuanlan.zhihu.com/p/20837097