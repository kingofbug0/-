# 1、HTML

- HTML:(Hyper TextMarkup Language) 超文本标记语言

- 文本:相当于就是记事本的文字,展示信息

- Web标准的构成  HTML 结构;CSS 表现;JS 行为

- | 标签名          | 定义       | 说明                                        |
  | --------------- | ---------- | ------------------------------------------- |
  | <html></html>   | HTML标签   | 页面中最大的标签,我们称为 **根标签**        |
  | <head></head>   | 文档的头部 | 注意在head标签中我们必须要设置的标签是title |
  | <title></title> | 文档的标题 | 让页面拥有一个属于自己的网页标题            |
  | <body></body>   | 文档的主体 | 元素包含文档的所有内容,页面内容存放在body中 |



##   常用标签

| 语义   | 标签                         |
| ------ | ---------------------------- |
| 加粗   | <strong></strong>或者<b></b> |
| 倾斜   | <em></em>或者<i></i>         |
| 删除线 | <del></del>或者<s></s>       |
| 下划线 | <ins></ins>>或者<u></u>      |

**根目录**:打开目录的第一层

## 超链接标签

语法:

```html
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
```

| 属性   | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| href   | 用于指定链接目标的url地址,(必须属性)当为标签应用href属性时,它就具有了超链接功能 |
| target | 用于指定链接页面的打开方式,其中_self为默认值,_blank为在新窗口中打开方式 |

### 链接分类

1. 外部链接

```html
<a href="http://www.baidu.com" target="_blank" >央视网消息:</a>
```

这里的央视网新闻就是一个超链接,点击后会跳转到百度的搜索引擎中去

blank是开启一个新标签,默认的值是_self 当前窗口打开,而_blank是开启一个新的窗口

​	2.内部链接

网站内部页面之间的相互链接

```html
<a href="HTML/.idea/第一个HTML.html" target="blank">神龟</strong><br/></a>
```

​	3.空链接

```html
<a href="#">作者</a>
```

​	4.下载链接

```html
 <a href="1.zip"><p>下载文件</p></a>
```

​	5.网页元素链接

​	6.锚点链接：就是直接跳转

- 在链接文本的href属性中，设置属性值为#名字的形式，如

  ```html
  <a href="#two">第2集</a>
  ```

- 找到目标位置标签,里面添加一个id属性=刚才的名字,如 

  ```html
  <h3 id="two">第二集介绍</h3>
  ```

- 比如

  ```html
  1.<a href="#经历">早年经历<br/></a>
     2.<a href="#运动">运动生涯<br/></a>
     3.<a href="#生涯">生涯数据<br/></a>
     4.<a href="#获奖">获奖记录<br/></a>
     <h3 id="经历">早年经历</h3>
  .....
     <h3 id="运动">运动生涯</h3>
  .....
     <h3 id="获奖">个人生活</h3>
  .....
  ```



## 注释

```html
<!-- 注释标签 -->
```

快捷键 ctrl+/

空格:

```html
&nbsp;
```

大于号:

```html
&gt;
```

小于号:

```html
&lt;
```

案例:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>第三个页面了已经</title>
</head>
<body>
   <h1 id="返回" style="text-align: center;"><strong>莱昂-梅西</strong></h1>
   <h3><a href="#早期">1.早期经历</a></h3>
   <h3><a href="#俱乐部">2.俱乐部生涯</a></h3>
   <h3><a href="#国家队">3.国家队生涯</a></h3>
<p>利昂内尔·梅西（Lionel Messi），全名利昂内尔·安德烈斯·梅西·库西蒂尼（Lionel Andrés Messi Cuccitini），昵称莱奥·梅西（Leo Messi），1987年6月24日出生于阿根廷圣菲省罗萨里奥，阿根廷职业足球运动员，司职前锋，现效力于法国足球甲级联赛的巴黎圣日耳曼足球俱乐部   。
2000年，梅西进入拉玛西亚青训营。2004年，梅西与<a href="https://baike.baidu.com/item/%E5%B7%B4%E5%A1%9E%E7%BD%97%E9%82%A3%E8%B6%B3%E7%90%83%E4%BF%B1%E4%B9%90%E9%83%A8/2431429?fromModule=lemma_inlink" target="_blank"> 巴塞罗那足球俱乐部 </a>签下职业合同  。2009年，梅西帮助巴萨加冕六冠王   ，个人首次荣膺金球奖  。2011年，梅西帮助巴萨加冕五冠王 。2012年，梅西以91粒正式比赛进球刷新足坛单一自然年进球纪录，连续第四年荣膺金球奖 。2015年，梅西再度帮助巴萨加冕五冠王，个人第五次荣膺金球奖  。2019年，梅西第六次荣膺金球奖。2021年，梅西自由加盟巴黎圣日耳曼足球俱乐部，同年第七次荣膺金球奖。
2005年，梅西帮助阿根廷U20青年队夺得世青赛冠军。2008年，梅西随阿根廷国奥队夺得北京奥运会男足金牌  。2014年，梅西帮助阿根廷国家队夺得世界杯亚军，个人荣膺世界杯金球奖 [20]  。2021年，梅西帮助阿根廷国家队夺得美洲杯冠军。2022年，梅西帮助阿根廷国家队夺得欧美杯冠军 。</p>
<img src="messi.jpg" height="400">

<br/> <h4 id="早期"><strong>早期经历</strong></h4>
<p>1987年，利昂内尔·梅西出生于阿根廷圣菲省罗萨里奥的一个工人阶级家庭  。四岁时，梅西加入由父亲豪尔赫·梅西执教的业余足球俱乐部格兰多利   。1994年，梅西加入纽维尔老男孩足球俱乐部少年队 [24]  。1997年，梅西被诊断出生长激素缺乏症。父亲的健康保险只承保两年的生长激素治疗，无法承担每月至少1000美元的治疗费用。纽维尔老男孩最初同意为梅西支付这笔费用，但最终因费用的不断增长而放弃 。
梅西与巴萨草签协议的纸巾
梅西与巴萨草签协议的纸巾
为了支付梅西的治疗费用，梅西的父亲联系住在西班牙加泰罗尼亚的亲戚申请到了当地的工作许可。2000年9月，梅西跟随父亲前往加泰罗尼亚的巴塞罗那足球俱乐部试训，并用表现征服了巴萨一线队主管卡洛斯·雷克萨奇。雷克萨奇力主签下梅西，但俱乐部董事会犹豫不决。12月14日，梅西与雷克萨奇在纸巾上草签了一份协议 。巴萨随即为梅西的父亲安排了一份工作，并承担了梅西的一部分治疗费用  。经过治疗，梅西的身高在2003年达到了1.69米  。</p>
<h4 id="俱乐部"><strong>俱乐部生涯</strong></h4>
<p>2001-02赛季
    <br/>巴萨生涯（2002-2010）
    <br/><a href="https://baike.baidu.com/pic/%E5%88%A9%E6%98%82%E5%86%85%E5%B0%94%C2%B7%E6%A2%85%E8%A5%BF/3965248/3928011646/d1a20cf431adcbef7609f06933fd39dda3cc7cd9311b?fr=lemma&fromModule=lemma_content-image&ct=cover#aid=3928011646&pic=d1a20cf431adcbef7609f06933fd39dda3cc7cd9311b" target="_blank">巴萨生涯（2002-2010）(41张)</a>
    <br/>2002年2月15日，梅西正式获得西班牙皇家足球协会的注册，成为拉玛西亚青训营的注册球员   ，与塞斯克·法布雷加斯和杰拉德·皮克成为队友 。
    <br/> 2002-03赛季
    <br/>2002-03赛季，梅西代表巴萨青年队在31场比赛中攻入38个进球，其中有9个梅开二度、4个帽子戏法和1个大四喜  ，帮助巴萨青年队夺得三项赛事的冠军。赛季结束后，梅西拒绝了阿森纳足球俱乐部的邀请，选择留在巴萨效力  。
    <br/>2003-04赛季
    <br/>2003年11月16日，在对阵波尔图足球俱乐部的友谊赛中，梅西在第75分钟身披14号球衣上场，上演巴萨一线队首秀  。
    <br/>2004年2月4日，梅西与巴萨签署第一份职业合同，合同期至2012年   。
    <br/>2003-04赛季，梅西共代表巴萨U19B队、U19A队、C队、B队和一线队出场37次，打入35个进球，帮助巴萨U19B队夺得联赛冠军  。
    <br/>2004-05赛季
    <br/>2004年7月20日，在对阵帕拉莫斯足球俱乐部的友谊赛中，梅西身披20号球衣斩获巴萨一线队首球，帮助球队6-0取胜  。10月初，主教练弗兰克·里杰卡尔德将梅西从B队提拔至一线队。由于罗纳尔迪尼奥已经在左路踢球，里杰卡尔德将梅西从习惯的左路和中路移至右边锋的位置  。10月16日，西甲第7轮客战皇家西班牙人足球俱乐部，梅西于第82分钟身披30号球衣替补登场，完成一线队正式比赛首秀 。12月7日，欧冠小组赛第6轮客战顿涅茨克矿工足球俱乐部，梅西职业生涯首次在一线队正式比赛中打满90分钟  。
    <br/>2005年5月1日，西甲第34轮主场对阵阿尔巴塞特足球俱乐部，梅西于第88分钟替补登场，并于第91分钟接罗纳尔迪尼奥的传球挑射破门，攻入职业生涯正式比赛首球，帮助球队2-0取胜  。
    <br/>2005年欧洲金童奖
    <br/>2004-05赛季，梅西代表巴萨在一线队正式比赛中出场9次，打入1球，随队夺得西甲冠军  ，个人荣膺2005年欧洲金童奖 、阿根廷足球先生  。
    <br/>2005-06赛季
    <br/>2005年6月，梅西与巴萨续约至2010年，违约金上涨至1.5亿欧元。9月，巴萨将合同到期时间修改为2014年，违约金为1.5亿欧元   。同月，梅西获得西班牙国籍，不再受西班牙足协关于非欧盟球员的名额限制  ，得以在西甲联赛中成为球队的主力右边锋，与罗纳尔迪尼奥、萨穆埃尔·埃托奥组成前场三叉戟  。11月2日，欧冠小组赛第3轮主场对阵帕纳辛奈科斯足球俱乐部，梅西收获欧冠处子球和职业生涯首个助攻，帮助球队5-0取胜  。
    <br/>2006年1月，在冬歇期重新注册后，梅西改穿19号球衣  。3月7日，欧冠1/8决赛次回合主场对阵切尔西足球俱乐部，梅西右大腿股二头肌撕裂，赛季报销  。
    <br/>2005-06赛季，梅西代表巴萨在各项正式比赛中出场25次，攻入8球，送出3个助攻，帮助巴萨夺得西班牙超级杯冠军、西甲冠军和欧冠冠军   ，个人荣膺2006年FIFPro年度最佳年轻球员 。</p>
<h4 id="国家队"><strong>国家队生涯</strong></h4>
2004年，时任阿根廷U20队主教练乌戈·托卡利在得知持有西班牙和阿根廷两国护照的梅西被西班牙U17队看中后，找到了阿根廷足协主席胡利奥·格隆多纳 ，格隆多纳决定让梅西尽快代表阿根廷出场   。6月24日，在阿根廷国青队（U20）对阵巴拉圭的友谊赛中，梅西身披17号球衣首次代表阿根廷出场  ，贡献两传一射，帮助阿根廷8-0取胜   。
<br/><p>蓝白生涯
<br/><a href="https://baike.baidu.com/pic/%E5%88%A9%E6%98%82%E5%86%85%E5%B0%94%C2%B7%E6%A2%85%E8%A5%BF/3965248/3929643280/738b4710b912c8fcc3ce12fb23538545d688d43f8bfe?fr=lemma&fromModule=lemma_content-image&ct=cover#aid=3929643280&pic=738b4710b912c8fcc3ce12fb23538545d688d43f8bfe" target="_blank">蓝白生涯(56张)</a>
<br/>2005年，梅西代表阿根廷参加南美青年足球锦标赛，在9场比赛中6次替补出场。梅西在与委内瑞拉的比赛中当选全场最佳球员，并在2-1力克巴西队的三四名决赛中打进制胜球，帮助阿根廷进军世青赛   。在夏天的荷兰世青赛中，梅西在首战负于美国队的比赛中未获首发机会。在之后的6场比赛中，梅西场场首发并斩获进球或助攻  ，并在决赛中完成梅开二度，帮助阿根廷夺得世青赛冠军，个人以6个进球夺得金靴奖，并荣膺世青赛金球奖 。
<br/>2005年8月17日，在客场对阵匈牙利的友谊赛中   ，梅西于第63分钟身披18号球衣替补登场，上演阿根廷国家队处子秀  。10月9日，世预赛南美区倒数第2轮主场对阵秘鲁，梅西首次为阿根廷国家队首发登场，并在比赛中造点，帮助阿根廷2-0取胜   。
<br/>2006年3月1日，在对阵克罗地亚的友谊赛中，梅西助攻卡洛斯·特维斯破门后斩获国家队处子球   。6月16日，2006年德国世界杯小组赛第2轮对阵塞黑，梅西替补登场上演世界杯首秀，成为阿根廷队史在世界杯出场年龄最小的球员   ，并贡献一传一射   。6月30日，世界杯1/4决赛客场对阵德国，梅西未获得登场机会，阿根廷在点球大战中负于对手，止步八强 [17]  。该届世界杯，梅西出场3次，贡献1个进球和1个助攻  。
<br/>2007年6月28日，2007年委内瑞拉美洲杯小组赛首轮，梅西助攻埃尔南·克雷斯波破门，帮助阿根廷4-1战胜美国   。7月8日，美洲杯1/4决赛，梅西破门，帮助阿根廷4-0战胜秘鲁  。7月11日，美洲杯半决赛，梅西破门，帮助阿根廷3-0战胜墨西哥   。7月15日，美洲杯决赛对阵巴西，梅西首发登场，阿根廷最终以0-3的比分告负，屈居亚军   。该届美洲杯，梅西登场6次，打入2个进球，送出1个助攻  ，个人被评为赛事最佳年轻球员  ，并入选赛事最佳阵容  。
<br/>2008年夏天，由于赛程与欧冠资格赛冲突，巴萨一度拒绝放走梅西参加2008年北京奥运会   。8月7日，奥运男足小组赛首轮，梅西贡献一传一射，帮助阿根廷2-1战胜科特迪瓦 。8月16日，奥运男足1/4决赛，梅西首开记录，并于加时阶段助攻安赫尔·迪马利亚完成绝杀，帮助阿根廷2-1战胜荷兰   。8月23日，奥运男足决赛对阵尼日利亚，梅西助攻迪马利亚打入全场唯一进球，帮助阿根廷1-0取胜夺冠  。
<br/>2009年3月28日，世预赛南美区第11轮  ，梅西迎来接过胡安·罗曼·里克尔梅的10号球衣的国家队首战暨迭戈·马拉多纳执教国家队的首场正式比赛 ，并在比赛中贡献一传一射，帮助阿根廷在主场4-0战胜委内瑞拉  。
<br/>2010年6月22日，2010年南非世界杯小组赛第3轮对阵希腊，梅西首次担任阿根廷国家队的场上队长，成为阿根廷队史最年轻的队长  。7月3日，世界杯1/4决赛，阿根廷0-4负于德国，止步八强  。该届世界杯，梅西5场全勤，贡献1个助攻   。</p>
<br/><a href="#返回">返回顶部</a>
</body>
</html>
```



## 表格

基本语法:

```html
<table>
	<tr>
		<td>单元格内的文字</td>定义表格中的单元格   表示tabled data表格数据
		...
	</tr>//表示行 镶嵌在<table>中
    ...
</table>    
```

th是表头单元格 会加粗居中

```html
<table align="center" width="500" height="250" border="1" cellspacing="0">//align=center代表表头居中 border=1是边框 cellspacing=0是无间隔
            <tr><th>姓名</th>   <th>性别</th>   <th>年龄</th> <th>相关链接</th></tr>
            <tr><td>梅西</td>   <td>男</td>   <td>35</td> <td><a href="https://baike.baidu.com/item/%E5%88%A9%E6%98%82%E5%86%85%E5%B0%94%C2%B7%E6%A2%85%E8%A5%BF/3965248" target="_blank">百度链接</a></td></tr>
            <tr><td>哈维</td>   <td>男</td>   <td>41</td><td><a href="https://baike.baidu.com/item/%E5%93%88%E7%BB%B4%E5%B0%94%C2%B7%E5%9F%83%E5%B0%94%E5%8D%97%E5%BE%B7%E6%96%AF%C2%B7%E5%85%8B%E9%9B%B7%E4%B9%8C%E6%96%AF/9597981?fromModule=lemma_search-box&fromtitle=%E5%93%88%E7%BB%B4&fromid=6819" target="_blank">百度链接</a></td></tr>
            <tr><td>伊涅斯塔</td>   <td>男</td>   <td>39</td><td><a href="https://baike.baidu.com/item/%E5%AE%89%E5%BE%B7%E9%9B%B7%E6%96%AF%C2%B7%E4%BC%8A%E6%B6%85%E6%96%AF%E5%A1%94?fromtitle=%E4%BC%8A%E6%B6%85%E6%96%AF%E5%A1%94&fromid=3071907&fromModule=lemma_search-box" target="_blank">百度链接</a></td></tr>
    </table>
```

### 合并单元格

- 跨行:colspan
- 跨列:rowspan

1. 找到目标单元格,写上合并方式=合并的单元格数量.如:<td colspan="2"></td>
2. 删除多余的单元格

## 列表标签

### 无序列表

<ul>表示html页面中项目的无序列表

基本语法格式如下:

```html
<ul>
	<li>列表1</li>
	<li>列表2</li>
	<li>列表3</li>
	...
</ul>	
```

注意:不能在ul中间直接添加字符

### 有序列表

<ol>
    <li>列表1</li>
    <li>列表2</li>
    <li>列表3</li>
</ol>


和无序列表使用差不多

### 自定义列表

<dl>
    <dt>名称1</dt>
    <dd>名词1解释1</dd>
    <dd>名词2解释2</dd>
</dl>

## input表单元素

 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表单元素</title>
</head>
<body>
    <form>
        <!-- 文本框里面可以输入任何文字 -->
        用户名:<input type="text" maxlength="8" name="username" > <br>
        <!-- password不显示作为密码比较好 -->
        密码:<input type="password" name="password"> <br>
        <!-- 单选按钮 -->

        性别:<input type="radio" name="sex" value="男">男 <input type="radio" name="sex" value="女">女<input type="radio" name="sex" value="猫">  猫猫
        <br>
        
        <!-- 多选按钮 -->
        <!-- checked属性就是默认打开后 勾选此项 -->
        爱好:<input type="checkbox" name="hobby" value="抽烟" checked="checked">抽烟<input type="checkbox" value="喝酒"name="hobby">喝酒 <input type="checkbox"value="打牌" name="hobby">打牌
        <br>
        
        <!-- submit是一个将元素上传的按钮 将表单域form中的元素值提交给后台数据 -->
        <input type="submit" value="登录">
        <input type="reset" value="重写输入">
        <br>
        <!-- file是一个文件域可以上传文件 -->
        <input type="file">
        <br>
        
        <!-- button是一个自定义的按钮 不会上传数据给后台 一般用于获取验证码之类的 -->
        <input type="button" value="获取验证码">
    </form>
</body>	
</html>


- name表单元素的名字,要求单选按钮和复选框要有相同的name值
- value是可以显示未填写格的提示文本

| 属性      | 属性值  | 描述                                                       |
| --------- | ------- | ---------------------------------------------------------- |
| name      | 自定义  | 定义input元素的名称 就是增加这个值后单选框就可以只选一个了 |
| value     | 自定义  | 规定input元素的值                                          |
| checked   | checked | 规定input元素首次加载时应当被选中                          |
| maxlength | 正整数  | 规定输入字段中的字符的最大长度                             |



### lebel标签

- label标签是用于当用户将鼠标移动到label范围的文本时,浏览器会自动将焦点转到对应的表单元素上 增加用户体验

- 语法

  ```html
  <label for="sex">男</label>
  
  <input type="radio" name="sex" id="sex" /> 
  <label for="sex"><input type="radio" name="sex" value="男" id="sex">男</label>
  与id对应使用 for和id要相对应
  ```



### select表单元素 

- 语法

  ```html
  <select>
  <option>选项1</option>
  <option>选项2</option>
  <option>选项3</option>
  <option>选项4</option>
  ...
  </select>
  ```

  select 一般也是放在域中使用 放在form中

### textarea表单元素

文本域,可以输入多行文字

- 语法

  ```html
  <textarea rows="3" cols="20">
  文本内容
  </textarea>
  ```



## 案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>注册页面</title>
</head>
<body>
    <strong><h2>都什么年代了 还在抽传统香烟</h2></strong>
    <table width="800"  cellspacing="0">
        <tr><td>性别</td>  <label for="sex">
                            <td><input type="radio" name="sex" value="男" id="sex">男
                            <input type="radio" name="sex" value="女" id="sex">女</td>
                            </label>
        </tr>
        <tr><td>生日</td>
                <td>
                <select>
                    <option>--请选择年--</option>
                    <option>1999</option>
                    <option>2000</option>
                    <option>2001</option>
                    <option>2002</option>
                    <option>2003</option>
                    <option>2004</option>
                </select>
                <select>
                    <option>--请选择月--</option>
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                    <option>6</option>
                    <option>7</option>
                    <option>8</option>
                    <option>9</option>
                    <option>10</option>
                    <option>11</option>
                    <option>12</option>
                </select>
                <select>
                    <option>--请选择日--</option>
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                    <option>6</option>
                    <option>7</option>
                    <option>8</option>
                    <option>9</option>
                    <option>10</option>
                    <option>11</option>
                    <option>12</option>
                    <option>没有您要的月份</option>
                </select>
                </td>       
        </tr>
        
       <tr>
        <td>所在地区</td>
        <td><select>
            <option>--请选择地区--</option>
            <option>四川</option>
            <option>贵州</option>
            <option>重庆</option>
            <option>西藏</option>
            <option>妈妈生的</option>
        </select></td>
       </tr> 

       <tr>
        <td>抽烟状况</td>

        <td>
            <input type="radio" name="hobby" value="电子烟">电子烟
            <input type="radio" name="hobby" value="传统香烟">传统香烟
            <input type="radio" name="hobby" value="混着抽 你懂吗">混着抽 你懂吗           
        </td>
       </tr>

       <tr>
           <td>学历</td>
           <td>
            <select>
                <option>--请选择学历--</option>
                <option>没读过书</option>
                <option>放马的含金量</option>
                <option>初中的含金量</option>
                <option>高中</option>
                <option>本科</option>
                <option>香烟研究生</option>
            </select>          
           </td>
       </tr> 

       <tr>
        <td>喜欢的香烟种类</td>
        <td>
            <input type="checkbox" name="type" value="喜贵">喜贵
            <input type="checkbox" name="type" value="玉溪">玉溪
            <input type="checkbox" name="type" value="华子">华子
            <input type="checkbox" name="type" value="锐克5代">锐克5代
        </td>
       </tr>

       <tr>
        <td>自我介绍</td>
        <td><textarea rows="2" cols="20"></textarea></td>
       </tr>

       <tr>
        <td></td>
        <td><input type="submit" value="登录"></td>
       </tr>

       <tr>
        <td></td>
        <td><input type="checkbox" value="同意" checked="checked">我同意免费注册 </td>
       </tr>

       <tr>
        <td></td>
        <td><a href="https://www.bilibili.com/video/BV1ZU4y1o7x5/" target="_blank">欢迎来到丁真宇宙!</a></td>
       </tr>

       <tr>
        <td></td>
        <td><h4>我承诺<h4>
            <ul>
                <li>抽电子烟只抽锐克5代</li>
                <li>每天早晨起来阿妈给我充电</li>
                <li>雪豹闭嘴</li>
                <li>不做讨口子</li>
            </ul> 
        <td>
       </tr>
    </table>
</body>
</html>
```



## 案例-2

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>手机问卷表单</title>
	<style type="text/css">
	table{border:double #333 2px}
	</style>
</head>
<body>
	<table align="center">
		<caption>手机问卷表单</caption>
		<tr>
			<td>姓名：</td>
			<td><input type="text" name="uname" size="30"></td>
		</tr>
		<tr>
			<td>Email：</td>
			<td><input type="email" name="email" size="30" value="username@mailsever.com"></td>
		</tr>
		<tr>
			<td>年龄：<input type="radio" name="age">未满20岁
			<input type="radio" name="age">20~29岁
			<input type="radio" name="age">30~39岁
			<input type="radio" name="age">40~49岁
			<input type="radio" name="age">50岁及以上
			</td>
		</tr>
		<tr>
			<td>使用的手机品牌：
				<input type="checkbox">诺基亚
				<input type="checkbox">摩托罗拉
				<input type="checkbox">爱立信
				<input type="checkbox">三星
			</td>
		</tr>
		<tr>
			<td>最常碰到的问题
			<textarea cols="10" rows="1"></textarea>
			</td>
		</tr>
		<tr>
			<td>使用手机网（可复选）
				<select>
					<option>中国电信</option>
					<option>中国联通</option>
					<option>中国移动</option>
				</select>
			</td>
		</tr>
		<tr>
			<td align="center">
				<input type="submit" value="提交">
    			<input type="reset" value="重填">
			</td>
		</tr>
	</table>
</body>
</html>

## 案例-3

<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>注册邮箱表单</title>
</head>
<body>
	<table>
		<form action="https://www.zhihu.com/zvideo/1553550902463721473">
			<tr>
				<td></td>
				<td>
				<input type="submit" name="free" value="注册免费邮箱">
				<input type="submit" name="vip" value="注册VIP邮箱">
				</td>
			</tr>
			<tr>
				<td>*邮箱地址</td>
				<td>
					<input type="text" name="uname" size="15"><inpyt type="text" name="lei" list="leix" size="5">
					<datalist id="liex">
						<option value="163.com"></option>
						<option value="126.com"></option>
						<option value="yeah.net"></option>
					</datalist>
				</td>
			</tr>
			<tr>
				<td></td>
				<td>6~16个字符，可以是数字，字母，下划线</td>
			</tr>
			<tr>
				<td>*密码：</td>
				<td>
					<input type="password" name="password">
				</td>
			</tr>
			<tr>
				<td></td>
				<td>6~16个字符，区分大小写</td>
			</tr>
			<tr>
				<td>*确认密码：</td>
				<td>
					<input type="password" name="password" >
				</td>
			</tr>
			<tr>
				<td></td>
				<td>请再次填写密码</td>
			</tr>
			<tr>
				<td>*验证码：</td>
				<td>
					<input type="text" name="number">
				</td>
			</tr>
			<tr>
				<td></td>
				<td>请填写图片中的字符，不区分大小写</td>
			</tr>
			<tr>
				<td>*手机号码：</td>
				<td>
					<input type="text" name="phonenumber">
				</td>
			</tr>
			<tr>
				<td></td>
				<td>请编辑短信：222发送到10690163222，以确保账户安全。（短信费用由运营商收取）</td>
			</tr>
			<tr>
				<td></td>
				<td>
					<input type="checkbox">同意《服务条款》、《隐私政策》和《儿童隐私政策》
				</td>
			</tr>
			<tr>
				<td></td>
				<td>
					 <input type="submit" value="已发送短信验证，立即登录"> 
				</td>
			</tr>
		</form>
	</table>
</body>
</html>
