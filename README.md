<h2> ISEE </h2>
  
---
这个网站是由我用[Node.js](http://nodejs.org)、[ejs](http://embeddedjs.com)、
[express](http://expressjs.com)和[Mongodb](http://mongodb.org)以及[UEditor](http://ueditor.baidu.com)
作为富文本编辑器而仓促做出来的。虽然能正常运行，但可能也会有bug之类的一些不可描述的问题，所以特此写下这个文档给
予后面维护的人。如果有对这些框架的使用不太熟悉的，可以去稍微了解下：
>nodejs  ejs  mongodb UEditor  Express

**网站架构**

* 主目录 ISEE
  + /config 内里有default.js文件，定义网站的端口之类的
  + /lib 内里有mongo.js和index.js  mongo.js是设数据库的，index.js是拿来用uedtior的
  + /logs  日志
  + /middlewares check中间件，判断是否登录
  + /models 内里存放着数据库的自定义函数
  + /node_modules npm依赖包
  + /public 样式和文件都存放在这
  + /routes nodejs的路由，里面是各个页面js路由处理
  + /views  前端页面，里面是各个页面的ejs模板
  + index.js 主程序文件
  + package.json 记录了网站的配置
---
**数据库**    

>lib/mongo.js

+ users
  - name
  - password       
  
  全局唯一的管理账号-_-只能通过内部用数据库直接设，当然你要弄多几个也完全OK
        
+ posts
  - title
  - content
  - file
  - img
  - type
  - participator
  - year
  - pic
  - <del>pv</del>   
  
 posts是关于proj和news的表。type是区分上传的是news还是project，img是在富文本编辑器中所贴的图的路径，file是上传附件的路径(二者不一样，
 即用附件上传的图是不会出现在正文，而是会以附件的形式出现的)，pic是projects页面的proj的小图的路径。至于命名
 的问题，因为测试时经常用重复的图，所以就照搬了UEditor的nodejs版本的处理方法，如果要改的话可以从
 /lib/index.js处修改。至于participator是proj的参与者，year是proj发表的年限，pv是阅读量-_-，感觉没什么鬼用。
        
+ members
  - name
  - engname
  - title
  - url
  - major
  - email
  - img
  - label
  - atitle
  
members是关于实验室成员的表。title是学位，输入时可以在create-member处选择。
url是个人主页，major是研究方向或者是专业, 随你喜欢-_-，label是区分是Student
抑或是Faculty，至于atitle则是Faculty的title，诸如教授之类的。
         
+ fileurl
  - url
  - type
  
  处理由富文本编辑器所上传的附件与图片的表，如果给予一个新的命名规则， 该表可以舍去。
  
---
**function**
> /model 中相应的 js文件   

讲道理的话看看函数名就能懂。

---


**前端架构**

就一堆ejs文件，结合/routes里面的路由文件看看就知道哪里调用那个了


---

**使用注意事项**

讲道理的话，暂时没发现有什么bug，但是在create-post界面，如果修改文章，必须要重新上传文件和贴图片，因为之前
想的是如果不这样做的话，先前的图片就会一直在服务器里面，删不掉。因为我的命名规则是<b>随机命名</b>，所以不好
直接做比对，当然维护的人设立一个命名规则，然后每次都去比对名字，通过名字来做删和不删，传与不传的选择也是可以。

---

**最后**

因为用的是以前没用过的nodejs，一个人写了一个多星期，在逻辑方面，可能会因为缺少与旁人的商讨而出现漏洞和破绽，
而且时间也并不宽裕，所以如若出现一些奇奇怪怪的问题，还请见谅。
                                                                                      
                                                                      ————312-东 陈子轩 2017.09.03
