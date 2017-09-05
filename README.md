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
        
+ posts (news or project)
 - title
 - content
 <br> news只由title和content组成，其中content中有所插入的图片地址。
 <br> 图片从ueditor上传到/img/posts/处，然后通过content调用，不需经过数据库。
 <br> 也可以在ueditor中编辑各种链接，可将文件放入/file/posts处(其实哪里都行)，然后再通过超链接下载或观看。
 - type (news or project)
 <br> 此属性自create后，就不再修改。
 - author
 - year
 - pic   
 - venue
 <br> project的属性，pic是在projects页面中出现的关于project的缩略图。
        
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
  
---
**function**
> /model 中相应的 js文件   

讲道理的话看看函数名就能懂。

---


**前端架构**

就一堆ejs文件，结合/routes里面的路由文件看看就知道哪里调用那个了


---

**使用注意事项**

讲道理的话，暂时没发现有什么bug，但是修改project(news不需要理会)和成员，必须要重新贴图片，因为如果不这样做，
那么先前修改前的图片就会一直在服务器里面，删不掉(<i>图片上传的时候会自己产生一个独立的id，无法比较两张图是否
同一张，而且不上传的话，提交时也会默认提交一个空文件</i>)。

---

**最后**

因为用的是以前没用过的node.js，一个人写了一个多星期，在逻辑方面，可能会因为缺少与旁人的商讨而出现漏洞和破绽，
而且时间也并不宽裕，所以如若出现一些奇奇怪怪的问题，还请见谅。
                                                                                      
                                                                      ————312-东 陈子轩 2017.09.06
