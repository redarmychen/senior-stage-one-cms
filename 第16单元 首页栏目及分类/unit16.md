首页栏目及分类

16.1 首页概览
----

首页是最复杂的一部分，首页往往是显示的内容庞杂，相互之间可能没有关联关系。

实现效果如下所示： 

 

![](media/80ee8dbf20352c192812c406d3c2169d.png) 

![](media/36f55d2e92774011ea4310ac09108c1b.png)

## 16.2 前端

### 16.2.1 要求

页面使用bootstrap+ jsp
实现即可。展示的内容包含频道列表、文章分类、文章列表、热门文章、最新文章、轮播图和用户登录状态等，如果需要可以再增加友情链接等等相关内容。

频道列表使用bootstrap 的样式实现，具体代码参考：

>    <ul class="list-group">
>    
>
>   ```html
>   <ul class="list-group">
>   <li class="list-group-item text-center"><a class="channel"
>   
>    href="/index">热门</a></li>
>   
>    。。。。。。。
>   
>   </ul>
>   
>   ```
>
>   ### 16.2.2 分类列表



分类列表使用使用bootstrap的nav 和nav-item样式实现，具体代码参考：

>   ```html
>    <ul class="nav">
>   
>    <!--栏目下所有 分类 -->
>   
>    <li class="nav-item list-group-item-success"><a class="nav-link"
>   
>    href="/index?chnId=${chnId}">全部</a></li>
>   
>    <li class="nav-item "><a class="nav-link"
>   
>    href="/index?chnId=1&catId=20">CBA</a></li>
>   
>    。。。。。。。。。。。
>   
>    </ul>
>   ```
>
>   

### 16.2.3 轮播图

轮播图参考bootstap官网即可。

### 16.2.4 用户登录状态

用户如果没有登录，右上角显示注册/登录链接，如果已经登录则显示用户的头像并且可以下拉菜单能够进入个人中心、退出系统等。判断是否登录的方式可以判断session中是否存在用户信息即可。这里的代码实现参考如下：



>   ```jsp
>    <ul class="nav">
>   
>    <c:choose>
>   
>    <%-- 登录显示用户菜单 --%>
>   
>    <c:when test="${sessionScope.SESSION_USER_KEY != null}">
>   
>    <li class="nav-item">
>   
>    <a class="nav-link" href="/my/home">
>   
>    <img alt="" src="/resource/images/default_avatar.png"
>    style="max-height: 2.5rem" class="rounded img-fluid">
>   
>    </a>
>   
>    </li>
>   
>    <li class="nav-item">
>   
>    <div class="dropdown" style="padding-top: 0.4rem;">
>   
>    <a href="#" class="nav-link dropdown-toggle" role="button"
>    id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true"
>    aria-expanded="false">
>   
>    <c:out value="${sessionScope.SESSION_USER_KEY.username}"
>    default="CMS-User"/>
>   
>    </a>
>   
>    <div class="dropdown-menu dropdown-menu-right"
>    aria-labelledby="dropdownMenuButton">
>   
>    <a class="dropdown-item" href="/">返回首页</a>
>   
>    <c:if test="${sessionScope.SESSION_USER_KEY.role==1}">
>   
>    <a class="dropdown-item" href="/admin/index">后台管理</a>
>   
>    </c:if>
>   
>    <c:if test="${sessionScope.SESSION_USER_KEY.role==0}">
>   
>    <a class="dropdown-item" href="/user/home">个人主页</a>
>   
>    </c:if>
>   
>    <a class="dropdown-item" href="#">个人设置</a>
>   
>    <a class="dropdown-item" href="#">我的文章</a>
>   
>    <div class="dropdown-divider"></div>
>   
>    <a class="dropdown-item" href="/user/logout">退出</a>
>   
>    </div>
>   
>    </div>
>   
>    </li>
>   
>    </c:when>
>   
>    <c:otherwise>
>   
>    <%-- 未登录显示登录注册链接 --%>
>   
>    <li class="nav-item"><a class="nav-link"
>    href="/user/register">注册</a></li>
>   
>    <li class="nav-item"><a class="nav-link"
>    href="/user/login">登录</a></li>
>   
>    </c:otherwise>
>   
>    </c:choose>
>   
>    </ul>
>   
>    </nav>
>   
>   ```
>
>   ## 16.3 后端 



### 16.3.1 控制层

获取首页数据，首页数据的获取包含栏目列表，当前栏目的分类以及当前栏目或分类下的文章列表。

为此定义Controller的函数为： 

![](media/e5f8184af0518960a3e46f1fbe5366c8.png) 

而函数中的具体实现如下：

![](media/cd3464d20b58159d2f2848d30f12c9cf.png) 

### 16.3.2 服务层

在首页中需要调用多个服务，主要有频道、分类、和文章，其中文章需要做分页处理。

##### 频道服务



![](media/d1b097deb4f10591d097f8e0ee939bd9.png) 



##### 分类服务

![](media/bf09bb43e1ea1f55928a6740b38e52bf.png) 

##### 文章列表

![](media/02c225fbd6b86b3cb63f7477ac9a5b8b.png) 

##### 热门文章

![](media/18633da8c3f2d1594f808a9c503888ba.png) 

##### 获取最新文章

![](media/2edba9e669fe6ab063690af895d91bab.png)

### 16.3.3 数据层

##### 	频道

![](media/05688876b4ed3a84260a2b92f6b6b42b.png) 

##### 	分类

![](media/6d0daed4b6cd84c427c5eefc09972a46.png) 

##### 	文章

>   ​          实体Bean主要属性如下：

![](media/6aeb027f052a75b3956f23029ef909eb.png) 

>      数据查询接口定义格式为：

![](media/1cc56f657f22ff96f26fa67be23c4b3a.png) 

>   对应的映射文件以及sql语句

![](media/0c2e92a411c440a92783d9bfb55e84d1.png) 

>   根据频道或者分类获取文章列表的sql语句：

![](media/c673243f2f1711ebb295c7d95f857b93.png) 

>   获取热门文章：

![](media/d80331fbd759eedad9fabf666dcdc4c6.png) 

>   获取最新文章：

![](media/bb75a32870ced858af77db1e7f29ea6d.png) 
