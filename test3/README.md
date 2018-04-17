# 实验3：图书管理系统领域对象建模
|学号|班级|姓名|照片|
|:-------:|:-------------: | :----------:|:---:|
|12345678|软件(本)15-4|赵卫东|![flow1](../01.jpg)|

## 1. 图书管理系统的类图

### 1.1 类图PlantUML源码如下：
<pre>
@startuml

package "图书馆系统的类图" #DDEEFF  {
    class 图书管理员{
                __ private data __
        	 	-用户名
        	 	-职工号
        	 	-- encrypted --
        	 	-密码
    }
    class 读者{
          __ private data __
          -用户名
          -身份证号
          -借书卡号
          -图书限额
          -以借图书数
          -- encrypted --
          -密码
    }
    class 查询图书{
         __ private data __
         -书名
         -ISBN号
    }
    class 登录{
           __ private data __
           -用户名
           -- encrypted --
           -密码

    }
    class 图书 {
            __ private data __
    	 	-书名
    	 	-ISBN号
    	 	-总量
    	 	-库存
    	 	-价格
    	 	-出版社
    	 	-简介
    	 	-作者
    	}

    class 借书记录 {
    		__ private data __
    	 	-读者姓名
    	 	-图书ISBN号
    	 	-借书日期
    	 	-归还日期
    	}
    class 逾期记录{
    	    __ private data __
    	    -逾期天数
    	}
    class 罚款细则{
            __ private data __
            -罚款金额
    	}

    	图书管理员 <|-- 登录
    	读者 <|-- 登录
    	图书管理员 "1" -- "N" 借书记录 : 登记
    	图书管理员 "1" -- "N" 图书 : 录入图书信息
    	读者 "1" -- "N" 借书记录 : 借还书
        读者 "1" -- "N" 查询图书 :是否可借
    	借书记录 "1"--"0..1" 逾期记录
    	逾期记录 "*"--"0..1" 罚款细则 : 使用
}
@enduml
</pre>
### 1.2 类图如下：

![](./libraryClass.png '图书馆系统类图')

### 1.3 类图说明：

读者和图书管理员都需要进行登录后才能执行具体操作。其中在归还图书时，系统将会对逾期记录通过罚款细则进行结算罚款金额。


## 2. 图书管理系统的对象图
### 2.1 类读者的对象图
#### 源码如下：
<pre>
@startuml
object 读者 #DDEEFF{
    username="wangzhaoliang"
    password="handsomewhite666"
    身份证号="513022199405200177"
    借书卡号="201510414416"
    图书限额=10
    已借图书数=3
}
@enduml
</pre>
#### 对象图如下：
![](./authorObject.png '图书馆系统类图')

### 2.2 类图书管理员的对象图
#### 源码如下：
<pre>
@startuml
object 图书管理员 #DDEEFF {
    username="admin"
    password="admin666"
    职工号="20151041"
}
@enduml
</pre>
#### 对象图如下：
![](./administratorsObject.png '图书馆系统类图')
### 2.3 类查询图书的对象图
#### 源码如下：
<pre>
@startuml
object 查询图书 #DDEEFF {
    书名="信息系统分析与设计（第4版）"
    ISBN="978-7-302-32982-4"
}
@enduml
</pre>
#### 对象图如下：
![](./querybookObject.png '图书馆系统类图')

### 2.4 类登录的对象图
#### 源码如下：
<pre>
@startuml
object 登录 #DDEEFF {
    username="wangzhaoliang"
    password="handsomewhite666"
}
@enduml
</pre>
#### 对象图如下：
![](./loginObject.png '图书馆系统类图')
### 2.5 类借书记录的对象图
#### 源码如下：
<pre>
@startuml
object 借书记录 #DDEEFF {
    读者姓名="王召亮"
    ISBN="978-7-302-32982-4"
    借书日期="2018-04-10"
    归还日期="2018-04-16"
}
@enduml
</pre>
#### 对象图如下：
![](./bookrecordObject.png '图书馆系统类图')

### 2.6 类图书的对象图
#### 源码如下：
<pre>
@startuml
object 图书 #DDEEFF {
    书名="信息系统分析与设计（第4版）"
    ISBN="978-7-302-32982-4"
    总量=60
    库存=40
    价格=36.00
    出版社="清华大学出版社"
    简介="本书可用作信息管理与信息系统、计算机应用、软件工程等专业的教材，也可供从事信息系统建设的技术人员、管理人员参考。"
    作者="王晓敏 邝孔武"
}
@enduml
</pre>
#### 对象图如下：
![](./bookObject.png '图书馆系统类图')
### 2.7 类逾期记录的对象图
#### 源码如下：
<pre>
@startuml
object 逾期记录 #DDEEFF{
    逾期天数=8
}
@enduml
</pre>
#### 对象图如下：
![](./overduerecordObject.png '图书馆系统类图')

### 2.8 类罚款细则的对象图
#### 源码如下：
<pre>
@startuml
object 罚款细则 #DDEEFF{
    罚款金额=2.80
}
@enduml
</pre>
#### 对象图如下：
![](./finerulesObject.png '图书馆系统类图')