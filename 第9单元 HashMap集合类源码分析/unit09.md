第九单元 HashMap&hashSet 源码分析
=================================

【授课重点】
============

1.  如何查看java的源码；

2.  通过查看HashMap类的属性,构造,核心函数读取\\存储\\删除来解析HashMap\\HashSet；

【考核要求】
============

1.  掌握hashMap的加载因子,扩容机制

2.  掌握hashMap的线程安全

3.  掌握hashMap的哈希值

4.  掌握hashMap的Entry数组

【教学内容】
============

课程导入
--------

### 学习源代码的益处

1.  能接触java的真实面貌

2.  能更早的进入到java大神的行列

3.  能够获取到更多面试机会

HashMap分析
-----------

### hashMap的底层存储

hashMap = 数组 +链表 + 红黑树

![1111](media/6313e48891ed71ea67b416edfc27e710.png)

### HashMap集合源码解析步骤

![](media/bb90bc7d372540d47320328f1cc8c764.png)

### 类的属性

![](media/538c4c8490c684397f70fa7e6cc8a51b.png)

### 类的构造方法

![](media/3935c1456775778badcdebb3b0de7378.png)

### 核心函数-存储

![](media/9aaeb15b2fa57cdc36f25afb85da569c.png)

### 核心函数-putVal方法执行过程

![](media/d74563a9d7e45467f942d4e02d95c925.png)

### 核心函数-存储思路

![](media/655f9179919463b8321f6649925302f5.png)

### 核心函数-扩容机制

resize前和resize后的元素布局如下

![](media/1d042d8588280ee6d641e3c9ce203f8c.png)

### 核心函数-读取

![](media/a3fc252858a4150f6dcdd49907da8dd2.png)

![](media/02415dfe2aab87a1ebadc2d457e98201.png)

### 小结

![](media/cf8074fa77dfe8b637c759b3763d9b49.png)

hashSet分析
-----------

### HashSet底层存储

HashSet是基于HashMap实现的，HashSet中的元素都存放在HashMap的
key上面，而value中的值都是统一的一个private static final Object PRESENT = new
Object();

### HashSet集合源码解析步骤

![](media/9926064dcedc097d99ac61a73daf5d4e.png)

### 类的属性

![](media/a3a08fae2ecdc93f71184bdef759fb3b.png)

### 类的构造方法

![](media/1dca7e218357ad98290bc67c4924b24c.png)

### 核心函数-存储

![](media/203bbfdc4ce6d543f6baefe40e673149.png)

### 核心读取

![](media/48d07e69bd9db24c9c9545eb012a47c5.png)

### 核心函数-删除

![](media/14d732af26524f3e1e4445dc52059ec6.png)

### 小结

![](media/747e40b5e67be9ba4ecd79fc48abf983.png)
