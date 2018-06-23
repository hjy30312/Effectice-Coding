# Effectice-Coding
个人对阿里巴巴Java开发手册 有关初学者必学的一些常用的规范的总结 不涉及并发、异常处理等 官方的很全面

源自：
- 中文版: *[阿里巴巴Java开发手册](https://github.com/alibaba/p3c/blob/master/%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4Java%E5%BC%80%E5%8F%91%E6%89%8B%E5%86%8C%EF%BC%88%E8%AF%A6%E5%B0%BD%E7%89%88%EF%BC%89.pdf)*
- [github地址](https://github.com/alibaba/p3c)
- [IDE插件文档](https://github.com/alibaba/p3c/wiki)

# 一、编程规约
## （一）命名风格

1. 【强制】代码中的命名均不能以<strong>下划线或美元符号</strong>开始，也不能以<strong>下划线或美元符号</strong>结束。
  <br><span style="color:red">反例</span>：`_name / __name / $name / name_ / name$ / name__`
2. 【强制】代码中的命名严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。 
  <br><span style="color:orange">说明</span>：正确的英文拼写和语法可以让阅读者易于理解，避免歧义。注意，即使纯拼音命名方式也要避免采用。 
  <br><span style="color:green">正例</span>：alibaba / taobao / youku / hangzhou 等国际通用的名称，可视同英文。 
  <br><span style="color:red">反例</span>：DaZhePromotion [打折] / getPingfenByName() [评分] / int 某变量 = 3 
3. 【强制】类名使用`UpperCamelCase`风格，但以下情形例外：DO / BO / DTO / VO / AO / PO等。 
 <br><span style="color:green">正例</span>：MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion 
 <br><span style="color:red">反例</span>：macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion 
4. 【强制】方法名、参数名、成员变量、局部变量都统一使用`lowerCamelCase`风格，必须遵从驼峰形式。 
<br><span style="color:green">正例</span>： localValue / getHttpMessage() / inputUserId 
5. 【强制】常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。 
<br><span style="color:green">正例</span>：MAX_STOCK_COUNT 
<br><span style="color:red">反例</span>：MAX_COUNT 
6. 【强制】抽象类命名使用Abstract或Base开头；异常类命名使用Exception结尾；测试类命名以它要测试的类名开始，以Test结尾。 
7. 【强制】类型与中括号紧挨相连来定义数组。 
 <br><span style="color:green">正例</span>：定义整形数组<code>int[] arrayDemo;</code> 
 <br><span style="color:red">反例</span>：在main参数中，使用<code>String args[]</code>来定义。 
8. 【强制】POJO类中布尔类型的变量，都不要加is前缀，否则部分框架解析会引起序列化错误。 
 <br><span style="color:red">反例</span>：定义为基本数据类型<code>Boolean isDeleted；</code>的属性，它的方法也是<code>isDeleted()</code>，RPC框架在反向解析的时候，“误以为”对应的属性名称是deleted，导致属性获取不到，进而抛出异常。
9. 【强制】包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，但是类名如果有复数含义，类名可以使用复数形式。 
 <br><span style="color:green">正例</span>：应用工具类包名为com.alibaba.ai.util、类名为MessageUtils（此规则参考spring的框架结构） 
10. 【强制】杜绝完全不规范的缩写，避免望文不知义。 
 <br><span style="color:red">反例</span>：AbstractClass“缩写”命名成AbsClass；condition“缩写”命名成 condi，此类随意缩写严重降低了代码的可阅读性。 
11. 【推荐】为了达到代码自解释的目标，任何自定义编程元素在命名时，使用尽量完整的单词组合来表达其意。 
<br><span style="color:green">正例</span>：从远程仓库拉取代码的类命名为PullCodeFromRemoteRepository。 
<br><span style="color:red">反例</span>：变量int a; 的随意命名方式。 
12. 【推荐】如果模块、接口、类、方法使用了设计模式，在命名时体现出具体模式。 
<br><span style="color:orange">说明</span>：将设计模式体现在名字中，有利于阅读者快速理解架构设计理念。 
<br><span style="color:green">正例</span>：
```
public class OrderFactory;
public class LoginProxy;
public class ResourceObserver; 
```
13. 【推荐】接口类中的方法和属性不要加任何修饰符号（public 也不要加），保持代码的简洁性，并加上有效的Javadoc注释。尽量不要在接口里定义变量，如果一定要定义变量，肯定是与接口方法相关，并且是整个应用的基础常量。 
<br><span style="color:green">正例</span>：接口方法签名void f(); 接口基础常量String COMPANY = "alibaba"; 
<br><span style="color:red">反例</span>：接口方法定义public abstract void f(); 
<br><span style="color:orange">说明</span>：JDK8中接口允许有默认实现，那么这个default方法，是对所有实现类都有价值的默认实现。 
14. 接口和实现类的命名有两套规则：  
   1）【强制】对于Service和DAO类，基于SOA的理念，暴露出来的服务一定是接口，内部的实现类用Impl的后缀与接口区别。 
   <br><span style="color:green">正例</span>：CacheServiceImpl实现CacheService接口。<br>
   2） 【推荐】 如果是形容能力的接口名称，取对应的形容词为接口名（通常是–able的形式）。
   <br><span style="color:green">正例</span>：AbstractTranslator实现 Translatable。 
16. 【参考】各层命名规约：  
  A) Service/DAO层方法命名规约<br>
   1） 获取单个对象的方法用get作前缀。
   <br>2） 获取多个对象的方法用list作前缀。
   <br>3） 获取统计值的方法用count作前缀。    
   4） 插入的方法用save/insert作前缀。    
   5） 删除的方法用remove/delete作前缀。    
   6） 修改的方法用update作前缀。 
  <br>B) 领域模型命名规约 <br>
   1） 数据对象：xxxDO，xxx即为数据表名。    
   2） 数据传输对象：xxxDTO，xxx为业务领域相关的名称。    
   3） 展示对象：xxxVO，xxx一般为网页名称。    
   4） POJO是DO/DTO/BO/VO的统称，禁止命名成xxxPOJO。 

## （二）常量定义

1. 【强制】不允许任何魔法值（即未经预先定义的常量）直接出现在代码中(使用常量类管理)。
<br><span style="color:red">反例</span>：
```
String key = "Id#taobao_" + tradeId;       
cache.put(key, value); 
```
2. 【强制】long或者Long初始赋值时，使用大写的L，不能是小写的l，小写容易跟数字1混淆，造成误解。 
<br><span style="color:orange">说明</span>：<pre>Long a = 2l;</pre> 写的是数字的`21`，还是Long型的`2`? 


## （三）代码格式
1. 【强制】大括号的使用约定。如果是大括号内为空，则简洁地写成`{}`即可，不需要换行；如果是非空代码块则：
<br>1） 左大括号前不换行。
<br>2） 左大括号后换行。
<br>3） 右大括号前换行。
<br>4） 右大括号后还有else等代码则不换行；表示终止的右大括号后必须换行。 
2. 【强制】 左小括号和字符之间不出现空格；同样，右小括号和字符之间也不出现空格。详见第5条下方正例提示。
<br><span style="color:red">反例</span>：
```
if (空格a == b空格)
```
3. 【强制】if/for/while/switch/do等保留字与括号之间都必须加空格。 
4. 【强制】任何二目、三目运算符的左右两边都需要加一个空格。 
   <br><span style="color:orange">说明</span>：运算符包括赋值运算符=、逻辑运算符&&、加减乘除符号等。
5. 【强制】采用4个空格缩进，禁止使用tab字符。 
   <br><span style="color:orange">说明</span>：
    如果使用tab缩进，必须设置1个tab为4个空格。IDEA设置tab为4个空格时，请勿勾选`Use tab character`；而在eclipse中，必须勾选`insert spaces for tabs`。 
   <br><span style="color:green">正例</span>： （涉及1-5点）

          public static void main(String[] args) {
              // 缩进4个空格
              String say = "hello";
              // 运算符的左右必须有一个空格
              int flag = 0;
              // 关键词if与括号之间必须有一个空格，括号内的f与左括号，0与右括号不需要空格
              if (flag == 0) {
                  System.out.println(say);
              }
              // 左大括号前加空格且不换行；左大括号后换行
              if (flag == 1) {
                  System.out.println("world");
                  // 右大括号前换行，右大括号后有else，不用换行
              } else {
                  System.out.println("ok");
                  // 在右大括号后直接结束，则必须换行
              }
          }

6. 【强制】注释的双斜线与注释内容之间有且仅有一个空格。 
 <br><span style="color:green">正例</span>：
```
// 这是示例注释，请注意在双斜线之后有一个空格  
String ygb = new String(); 
```
7. 【强制】单行字符数限制不超过120个，超出需要换行，换行时遵循如下原则：
<br>1）第二行相对第一行缩进4个空格，从第三行开始，不再继续缩进，参考示例。
<br>2）运算符与下文一起换行。
<br>3）方法调用的点符号与下文一起换行。
<br>4） 方法调用时，多个参数，需要换行时，在逗号后进行。
<br>5） 在括号前不要换行，见反例。
<br><span style="color:green">正例</span>：
```
StringBuffer sb = new StringBuffer();
     // 超过120个字符的情况下，换行缩进4个空格，点号和方法名称一起换行
    sb.append("zi").append("xin")...
                   .append("huang")...
                   .append("huang")...
                   .append("huang");
```
<br><span style="color:red">反例</span>：
```
StringBuffer sb = new StringBuffer();  
// 超过120个字符的情况下，不要在括号前换行  
sb.append("zi").append("xin")...append      
("huang");    
// 参数很多的方法调用可能超过120个字符，不要在逗号前换行  
method(args1, args2, args3, ... 
, argsX); 
```
8. 【强制】方法参数在定义和传入时，多个参数逗号后边必须加空格。 
<br><span style="color:green">正例</span>：下例中实参的"a",后边必须要有一个空格。 
```
method("a", "b", "c"); 
```
9. 【强制】IDE的text file encoding设置为UTF-8; IDE中文件的换行符使用Unix格式，不要使用Windows格式。 

11. 【推荐】不同逻辑、不同语义、不同业务的代码之间插入一个空行分隔开来以提升可读性。 
<br><span style="color:orange">说明</span>：没有必要插入**多个空行**进行隔开。 

## (四) OOP规约 

1. 【强制】避免通过一个类的对象引用访问此类的静态变量或静态方法，无谓增加编译器解析成本，直接用**类名**来访问即可。 
2. 【强制】所有的覆写方法，必须加@Override注解。 
<br><span style="color:orange">说明</span>：getObject()与get0bject()的问题。一个是字母的O，一个是数字的0，加@Override可以准确判断是否覆盖成功。另外，如果在抽象类中对方法签名进行修改，其实现类会马上编译报错。 

 
5. 【强制】不能使用过时的类或方法。 
<br><span style="color:orange">说明</span>：java.net.URLDecoder 中的方法decode(String encodeStr) 这个方法已经过时，应该使用双参数decode(String source, String encode)。接口提供方既然明确是过时接口，那么有义务同时提供新的接口；作为调用方来说，有义务去考证过时方法的新实现是什么。 
6. 【强制】Object的equals方法容易抛空指针异常，应使用常量或确定有值的对象来调用equals。
<br><span style="color:green">正例</span>："test".equals(object);
<br><span style="color:red">反例</span>：object.equals("test"); 
<br><span style="color:orange">说明</span>：推荐使用java.util.Objects#equals（JDK7引入的工具类）
7. 【强制】所有的相同类型的包装类对象之间值的比较，全部使用equals方法比较。 
<br><span style="color:orange">说明</span>：对于Integer var = ?  在-128至127范围内的赋值，Integer对象是在IntegerCache.cache产生，会复用已有对象，这个区间内的Integer值可以直接使用==进行判断，但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象，这是一个大坑，推荐使用equals方法进行判断。 
 
9. 【强制】定义DO/DTO/VO等POJO类时，不要设定任何属性**默认值**。
<br><span style="color:red">反例</span>：POJO类的gmtCreate默认值为new Date();但是这个属性在数据提取时并没有置入具体值，在更新其它字段时又附带更新了此字段，导致创建时间被修改成当前时间。  
11. 【强制】构造方法里面禁止加入任何业务逻辑，如果有初始化逻辑，请放在init方法中。 
12. 【强制】POJO类必须写toString方法。使用IDE中的工具：source> generate toString时，如果继承了另一个POJO类，注意在前面加一下super.toString。 <br><span style="color:orange">说明</span>：在方法执行抛出异常时，可以直接调用POJO的toString()方法打印其属性值，便于排查问题。 

14. 【推荐】当一个类有多个构造方法，或者多个同名方法，这些方法应该按顺序放置在一起，便于阅读，此条规则优先于第15条规则。 
15. 【推荐】 类内方法定义的顺序依次是：公有方法或保护方法 > 私有方法 > getter/setter方法。
<br><span style="color:orange">说明</span>：公有方法是类的调用者和维护者最关心的方法，首屏展示最好；保护方法虽然只是子类关心，也可能是“模板设计模式”下的核心方法；而私有方法外部一般不需要特别关心，是一个黑盒实现；因为承载的信息价值较低，所有Service和DAO的getter/setter方法放在类体最后。 
16. 【推荐】setter方法中，参数名称与类成员变量名称一致，this.成员名 = 参数名。在getter/setter方法中，不要增加业务逻辑，增加排查问题的难度。
<br><span style="color:red">反例</span>：
```
  public Integer getData() {      
      if (condition) {  
        return this.data + 100;  
      } else { 
        return this.data - 100; 
      }  
  }
```
17. 【推荐】循环体内，字符串的连接方式，使用StringBuilder的append方法进行扩展。
<br><span style="color:orange">说明</span>：反编译出的字节码文件显示每次循环都会new出一个StringBuilder对象，然后进行append操作，最后通过toString方法返回String对象，造成内存资源浪费。  <br><span style="color:red">反例</span>：
```
  String str = "start";
  for (int i = 0; i < 100; i++) {
      str = str + "hello";      
  }
```
18. 【推荐】final可以声明类、成员变量、方法、以及本地变量，下列情况使用final关键字：
<br>1） 不允许被继承的类，如：String类。
<br>2） 不允许修改引用的域对象，如：POJO类的域变量。
<br>3） 不允许被重写的方法，如：POJO类的setter方法。
<br>4） 不允许运行过程中重新赋值的局部变量。
<br>5） 避免上下文重复使用一个变量，使用final描述可以强制重新定义一个变量，方便更好地进行重构。 


## (七) 控制语句 
1. 【强制】在一个switch块内，每个case要么通过break/return等来终止，要么注释说明程序将继续执行到哪一个case为止；在一个switch块内，都必须包含一个default语句并且放在最后，即使空代码。 
2. 【强制】在if/else/for/while/do语句中必须使用大括号。即使只有一行代码，避免采用单行的编码方式：
<pre>if (condition) statements;</pre>
3. 【强制】在高并发场景中，避免使用”等于”判断作为中断或退出的条件。 
<br><span style="color:orange">说明</span>：如果并发控制没有处理好，容易产生等值判断被“击穿”的情况，使用大于或小于的区间判断条件来代替。  
<br><span style="color:red">反例</span>：判断剩余奖品数量等于0时，终止发放奖品，但因为并发处理错误导致奖品数量瞬间变成了负数，这样的话，活动无法终止。 

5. 【推荐】除常用方法（如getXxx/isXxx）等外，不要在条件判断中执行其它复杂的语句，将复杂逻辑判断的结果赋值给一个有意义的布尔变量名，以提高可读性。 
<br><span style="color:orange">说明</span>：很多if语句内的逻辑相当复杂，阅读者需要分析条件表达式的最终结果，才能明确什么样的条件执行什么样的语句，那么，如果阅读者分析逻辑表达式错误呢？ <br><span style="color:green">正例</span>： 
```
// 伪代码如下 final boolean existed = (file.open(fileName, "w") != null) && (...) || (...); 
if (existed) {    
   ... 
}  
```  
<span style="color:red">反例</span>：
```
if ((file.open(fileName, "w") != null) && (...) || (...)) {     
  ... 
}
```
6. 【推荐】循环体中的语句要考量性能，以下操作尽量移至循环体外处理，如定义对象、变量、获取数据库连接，进行不必要的try-catch操作（这个try-catch是否可以移至循环体外）。 
7. 【推荐】避免采用取反逻辑运算符。 
<br><span style="color:orange">说明</span>：取反逻辑不利于快速理解，并且取反逻辑写法必然存在对应的正向逻辑写法。 
<br><span style="color:green">正例</span>：使用if (x < 628) 来表达 x 小于628。
<br><span style="color:red">反例</span>：使用if (!(x >= 628)) 来表达 x 小于628。

# 五、MySQL数据库
## (一) 建表规约
1. 【强制】表达是与否概念的字段，必须使用is_xxx的方式命名，数据类型是unsigned tinyint（ 1表示是，0表示否）。 
<br><span style="color:orange">说明</span>：任何字段如果为非负数，必须是`unsigned`。 
<br><span style="color:green">正例</span>：表达逻辑删除的字段名`is_deleted`，1表示删除，0表示未删除。 
2. 【强制】表名、字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑。 <br><span style="color:orange">说明</span>：MySQL在Windows下不区分大小写，但在Linux下默认是区分大小写。因此，数据库名、表名、字段名，都不允许出现任何大写字母，避免节外生枝。 <br><span style="color:green">正例</span>：aliyun_admin，rdc_config，level3_name <br><span style="color:red">反例</span>：AliyunAdmin，rdcConfig，level_3_name 
3. 【强制】表名不使用复数名词。 
<br><span style="color:orange">说明</span>：表名应该仅仅表示表里面的实体内容，不应该表示实体数量，对应于DO类名也是单数形式，符合表达习惯。 
4. 【强制】禁用保留字，如`desc`、`range`、`match`、`delayed`等，请参考MySQL官方保留字。 
5. 【强制】主键索引名为pk_字段名；唯一索引名为uk_字段名；普通索引名则为idx_字段名。 
<br><span style="color:orange">说明</span>：pk_ 即primary key；uk_ 即 unique key；idx_ 即index的简称。 
6. 【强制】小数类型为decimal，禁止使用float和double。 
<br><span style="color:orange">说明</span>：float和double在存储的时候，存在精度损失的问题，很可能在值的比较时，得到不正确的结果。如果存储的数据范围超过decimal的范围，建议将数据拆成整数和小数分开存储。 
7. 【强制】如果存储的字符串长度几乎相等，使用char定长字符串类型。 
8. 【强制】varchar是可变长字符串，不预先分配存储空间，长度不要超过5000，如果存储长度大于此值，定义字段类型为text，独立出来一张表，用主键来对应，避免影响其它字段索引效率。 
10. 【推荐】表的命名最好是加上“业务名称_表的作用”。 
<br><span style="color:green">正例</span>：alipay_task / force_project / trade_config 

13. 【推荐】字段允许适当冗余，以提高查询性能，但必须考虑数据一致。冗余字段应遵循：  
1）不是频繁修改的字段。  
2）不是varchar超长字段，更不能是text字段。
 <br><span style="color:green">正例</span>：商品类目名称使用频率高，字段长度短，名称基本一成不变，可在相关联的表中冗余存储类目名称，避免关联查询。 
15. 【参考】合适的字符存储长度，不但节约数据库表空间、节约索引存储，更重要的是提升检索速度。 <br><span style="color:green">正例</span>：如下表，其中无符号值可以避免误存负数，且扩大了表示范围。 

| 对象  | 年龄区间 | 类型  | 字节  |
| ------------- |:-------------| :----- |:----- |
| 人 |150岁之内  | unsigned tinyint|1|
| 龟 |数百岁 | unsigned smallint |2|
| 恐龙化石 |数千万岁 | unsigned int |4|
| 太阳 |约50亿年 | unsigned bigint |8|

## (三) SQL语句 
1. 【强制】不要使用count(列名)或count(常量)来替代count(*)，count(*)是SQL92定义的标准统计行数的语法，跟数据库无关，跟NULL和非NULL无关。 
<br><span style="color:orange">说明</span>：count(*)会统计值为NULL的行，而count(列名)不会统计此列为NULL值的行。 
2. 【强制】count(distinct col) 计算该列除NULL之外的不重复行数，注意 count(distinct col1, col2) 如果其中一列全为NULL，那么即使另一列有不同的值，也返回为0。 
3. 【强制】当某一列的值全是NULL时，count(col)的返回结果为0，但sum(col)的返回结果为NULL，因此使用sum()时需注意NPE问题。 
<br><span style="color:green">正例</span>：可以使用如下方式来避免sum的NPE问题：
<pre>SELECT IF(ISNULL(SUM(g)),0,SUM(g)) FROM table; </pre>
4. 【强制】使用`ISNULL()`来判断是否为NULL值。 说明：NULL与任何值的直接比较都为NULL。  
1） `NULL<>NULL`的返回结果是NULL，而不是`false`。  
2） `NULL=NULL`的返回结果是NULL，而不是`true`。  
3） `NULL<>1`的返回结果是NULL，而不是`true`。 
5. 【强制】 在代码中写分页查询逻辑时，若count为0应直接返回，避免执行后面的分页语句。
8. 【强制】数据订正（特别是删除、修改记录操作）时，要先select，避免出现误删除，确认无误才能执行更新语句。 
10. 【参考】如果有全球化需要，所有的字符存储与表示，均以utf-8编码，注意字符统计函数的区别。 
<br><span style="color:orange">说明</span>：
<pre>SELECT LENGTH("轻松工作")； 返回为12
SELECT CHARACTER_LENGTH("轻松工作")； 返回为4</pre>
如果需要存储表情，那么选择utf8mb4来进行存储，注意它与utf-8编码的区别。 

# 六、工程结构
## (一) 应用分层 

1. 【推荐】图中默认上层依赖于下层，箭头关系表示可直接依赖，如：开放接口层可以依赖于Web层，也可以直接依赖于Service层，依此类推：
 ![应用分层](https://github.com/alibaba/p3c/blob/master/p3c-gitbook/images/alibabaLevel.png)
 - 开放接口层：可直接封装Service方法暴露成RPC接口；通过Web封装成http接口；进行网关安全控制、流量控制等。 
 - 终端显示层：各个端的模板渲染并执行显示的层。当前主要是velocity渲染，JS渲染，JSP渲染，移动端展示等。 
 - Web层：主要是对访问控制进行转发，各类基本参数校验，或者不复用的业务简单处理等。 
 - Service层：相对具体的业务逻辑服务层。 
 - Manager层：通用业务处理层，它有如下特征：
 <br>1） 对第三方平台封装的层，预处理返回结果及转化异常信息；
 <br>2） 对Service层通用能力的下沉，如缓存方案、中间件通用处理；
 <br>3） 与DAO层交互，对多个DAO的组合复用。
 - DAO层：数据访问层，与底层MySQL、Oracle、Hbase等进行数据交互。 
 - 外部接口或第三方平台：包括其它部门RPC开放接口，基础平台，其它公司的HTTP接口。

3. 【参考】分层领域模型规约：
  - DO（Data Object）：与数据库表结构一一对应，通过DAO层向上传输数据源对象。
  - DTO（Data Transfer Object）：数据传输对象，Service或Manager向外传输的对象。
  - BO（Business Object）：业务对象。由Service层输出的封装业务逻辑的对象。
  - AO（Application Object）：应用对象。在Web层与Service层之间抽象的复用对象模型，极为贴近展示层，复用度不高。
  - VO（View Object）：显示层对象，通常是Web向模板渲染引擎层传输的对象。
  - Query：数据查询对象，各层接收上层的查询请求。注意超过2个参数的查询封装，禁止使用Map类来传输。
