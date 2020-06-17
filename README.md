# Coldcalls & Messages

本项目类似于轰炸机。<br>
逻辑如下：
- 使用手机号在留学、在线教育类网站留下信息，则销售会主动不厌其烦地call此手机号。
- 使用手机号注册、登录网站，则会收到短信验证码。
<br>

### 食用方式
- 项目基于selenium，请下载对应版本chromedriver放于本项目下
```bash
git clone https://github.com/broholens/coldcalls.git
cd coldcalls
pip install requiremenrts.txt
python cold_call.py
```
- **添加自己解析的网站**<br>
编辑*sites.json*，按照解析规则添加关键字即可。**欢迎Pull-Request，提供更多网站的解析。**<br><br>
解析规则如下：

| 关键字 | 说明 | 示例 |
| :-----: | :----: | :----: |
| url | 网站url | https://qy.thea.cn/ |
| rate | 网站每天请求次数。不填默认为1。电话类建议不填，短信类视网站规则填写 | 3 |
| sleep_time | 访问网站后等待页面加载时间，不填默认为0 | 2 |
| iframe | 需要切换的iframe，不切换则不填 | LR_miniframe |
| preset | 请求到网站后，填写表单前需要做的操作。 没有则不填|  |
| username_path | 用户名填写，没有则不填 |  |
| phone_path | 手机号填写 |  |
| message_path | 留言填写，没有则不填 |  |
| password_path | 密码填写，没有则不填 |  |
| password_confirm_path | 密码确认填写，没有则不填 |  |
| submit_path | 提交表单按钮，没有则不填 |  |
| postset | 表单提交完后需要做的操作。 没有则不填|  |
| mode | 定位元素的模式，可选值[id、xpath、name、class_name、link_text]，默认为xpath，调用selenium对应方法 | id |
| value | 按照mode定位的关键字 | mobile |
| type | 仅支持preset和postset，可选值[click、script]，默认为click，执行点击操作；script则执行value对应的脚本，不必填mode字段 | script |

- 示例
```json
  {
    "rate": 3,
    "sleep_time": 3,
    "url": "https://qy.thea.cn/",  
    "iframe": "LR_miniframe",
    "preset": {
      "type": "click",
      "mode": "xpath",
      "value": "//li[@class=\"clearfix\"]/div/a[2]"
    },
    "username_path": {
      "mode": "name",  
      "value": "contact"
    },
    "phone_path": {
      "mode": "name",
      "value": "mobile"
    },
    "password_path": {
      "mode": "name",
      "value": "password"
    },
    "password_confirm_path": {
      "mode": "name",
      "value": "password_confirm"
    },
    "message_path": {
      "mode": "name",
      "value": "content"
    },
    "submit_path": {
      "value": "//div[@class=\"qpform\"]//input[last()]"
    },
    "postset": {
      "type": "script",
      "value": "FunLM10GetPrice()"
    }
  }
```
- 解析网站关键字执行顺序<br>
**`url -> sleep_time -> iframe -> preset -> *_path -> postset`**

### 已解析网站列表

1. [liuxue86](https://www.liuxue86.com/)
2. [北木](http://www.beimu.com/school/)
3. [伯乐](http://www.bole.com/registerPage)
4. [课工厂](http://www.kgc.cn/zhuanti/cpjh_pc.shtml)
5. [创思童](http://www.gemstonecn.com/consociation.php)
6.  [诺达名师](http://qy.thea.cn/)
7. [掌门一对一](https://www.zhangmen.org/lp/sem)
8. [加盟1对1](http://zs.jiameng.com/goJmPriceBoard2.html)
9. [秦学100](http://fd1.qinxue100.com/index.html)
10. [英孚](https://www.ef.com.cn/englishfirst/kids/)
11. [趣趣abc](https://www.ququabc.com/offlinep.htm)
12. [乐宁](http://learning.learningedu.com.cn/)


<!--
1.  [乐宁](http://learning.learningedu.com.cn/)
2.  [七彩星球](http://www.cctvqcxq.com/)
3.  [讲吧秀](http://www.jbajy.com/jbx/)
4.  [素质家](http://siwei.haike100.com/)
5.  [小码教育](http://ks.xiaoma.cn/ks/tgxa/baidu/)
6.  [阿童木](http://m.atomdiy.com/atm_09_bd5/)
7.  [昂立教育](http://www.onlychild.cn/)
8.  [久伴英语](http://www.biteabc.com/)
9.  [芝麻街英语](http://www.sesamestreetenglishchina.com/)
10. [51talk](http://www.51talk.com/landing/bdpz1_087737.html)
11. [山姆大叔少儿英语](http://www.unclesamedu.com/index.php)
12. [学而思](https://zt.xueersi.com/zaixian/pc-zhu-tiyanke/index.html)
13. [汤姆客](http://www.hellotom-edu.com/Index/tree/id/470)
14. [勤学教育](http://www.qinxue365.com/business/388.html)
15. [创业盟](http://bdjy.zsyekuf.cn/pc/publicity1)
16. [it61](http://www.it61.cn/coding-class/)
17. [傲梦](https://all-dream.com/)
18. [vipcode](https://www.vipcode.com/)
19. [优学](http://www.ubxedu.com/course/)
20. [码高](http://www.magaoedu.cn/)
21. [小码王](http://www.xiaomawang.net/)
22. [有渔](http://www.youyucode.com/)
23. [达内](http://xa.ui.tedu.cn/baiduuipc/zh/)
24. [米德](https://www.midebc.cn/)
25. [趣码](http://xw7c8v4rx7ajxxvj.mikecrm.com/kiMGSiQ)
26. [百姓网](http://www.baixing.com/oz/verify/reg)
27. [58登陆](https://passport.58.com/login)
28. [58注册](https://passport.58.com/reg)
29. [快递100登陆](https://sso.kuaidi100.com/sso/authorize.do)
30. [快递100注册](https://sso.kuaidi100.com/sso/reg.jsp)
31. [鲸鱼小班](https://www.jingyuxiaoban.com/app/register)
32. [沪江](https://class.hujiang.com/)
33. [知网](http://my.cnki.net/Register/CommonRegister.aspx)
34. [建设](http://member.jianshe99.com/member/register.shtm)
35. [华图](http://v.huatu.com/newUser/reg.php)
36. [乐乐课堂](http://www.leleketang.com/login/register.php)
37. [赶考网](https://www.gankao.com/user/create)
38. [融易富](https://www.993261.com/account/register)
39. [恒丰优配](http://www.pz1997.com/register)
40. [教育联展网](https://www.thea.cn/zt/erjian/)
41. [无忧考网](https://user.51test.net/user/reg.html)
42. [高思教育](https://www.gaosiedu.com/#/loginCode)
43. [vipjr](https://www.vipjr.com/)
44. [千里马](http://www.qianlima.com/new/keywordzhuolu_invite.jsp)
45. [编程猫](https://hi.codemao.cn/v2)
-->
