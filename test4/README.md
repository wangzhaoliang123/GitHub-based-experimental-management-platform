# 实验4：图书管理系统顺序图绘制
|    学号  |   班级    |    姓名  |   照片     |
|:--------:|:--------: | :----------: | :-------:|
|201510414416|软件(本)15-4|王召亮 |![](./01.jpg '666')|

## 图书管理系统的顺序图

## 1. 查询图书用例
## 1.1. 查询图书用例PlantUML源码

<pre>
 @startuml
        autonumber
        skinparam sequenceParticipant underline
        actor "：读者" as User #black
        note left of User #bbb
            读者查找图
            书顺序图
        end note
        participant "：查询图书" as A
        participant "：图书" as B
        User -[#red]> A:查找图书信息
        activate User
        activate A
        activate B
        A -[#red]> B: 根据图书编号查找图书
        B -[#red]> A: 返回图书信息
        deactivate User
        deactivate B
        A -[#red]>User:显示图书信息
        activate User
        deactivate User
        deactivate A
@enduml
</pre>

## 1.2. 查询图书用例顺序图
![](./queryBook.png '查询图书顺序图')

## 1.3. 查询图书用例顺序图说明
读者通过图书编号查找图书，查找到的图书会反馈信息给读者。显示图书的状态信息（包括数目、是否可借等）。

***

## 2. 借书用例
## 2.1. 借书用例PlantUML源码

<pre>
@startuml
autonumber
        skinparam sequenceParticipant underline
        actor "：图书管理员" as admin #black
        note left of admin #bbb
            借阅图书
           用例顺序图
        end note
         participant "：读者" as reader
         participant "：资源项" as resource
         participant "：馆藏资源品种" as resourceVariety
         participant "：借书记录" as borrowRecord
         admin -[#red]> reader:验证读者
         activate admin
         activate reader
         deactivate reader
         admin -[#red]> reader:取读者限额
         activate reader
         deactivate reader
         loop
            admin -[#red]> resource:获取资源项
            activate resource
            resource -[#red]> resourceVariety:查找资源品种
            activate resourceVariety
            deactivate resource
            deactivate resourceVariety
            admin -[#red]> borrowRecord:创建借书记录
            activate borrowRecord
            deactivate borrowRecord
            admin -[#red]> resource:借出资源
            activate resource
            resource -[#red]> resourceVariety:减少可借数量
            activate resourceVariety
            deactivate resource
            deactivate resourceVariety
            admin -[#red]> reader:减少可用限额
            activate reader
            deactivate reader
         end
         admin -[#red]> borrowRecord:打印借书清单
         activate borrowRecord
         deactivate borrowRecord
         deactivate admin

@enduml
</pre>

## 2.2. 借书用例顺序图
![](./borrowBook.png '借阅图书顺序图')

## 2.3. 借书用例顺序图说明
借书之前管理员会验证读者是否可借图书或可借图书数量，然后查找图书种类，创建借书记录。借书后，可借数量减少。最后图书管理员打印借书清单。

***

## 3. 还书用例
## 3.1. 还书用例PlantUML源码

<pre>
@startuml
autonumber
        skinparam sequenceParticipant underline
        actor "：图书管理员" as admin #black
        note left of admin #bbb
            归还图书
           用例顺序图
        end note
         participant "：资源项" as resource
         participant "：借书记录" as borrowRecord
         participant "：馆藏资源品种" as resourceVariety
         participant "：读者" as reader
         participant "：逾期记录" as overdueRecord
         admin -[#red]> resource:读取资源信息
         activate admin
         activate resource
         resource -[#red]> borrowRecord:取借书记录
         activate borrowRecord
         deactivate borrowRecord
         resource -[#red]> resourceVariety:取资源的品种
         activate resourceVariety
         deactivate resourceVariety
         deactivate resource
         admin -[#red]> reader:取借阅者信息
         activate reader
         deactivate reader
         admin -[#red]> resource:归还资源
         activate resource
         resource -[#red]> resourceVariety:增加可借数量
         activate resourceVariety
         deactivate resourceVariety
         deactivate resource
         admin -[#red]> borrowRecord:登记还书日期
         activate borrowRecord
         deactivate borrowRecord
         opt 逾期
            admin -[#red]> overdueRecord:登记逾期记录
            activate overdueRecord
            deactivate overdueRecord
            deactivate admin
         end

@enduml
</pre>

## 3.2. 还书用例顺序图
![](./returnBook.png '归还图书顺序图')

## 3.3. 还书用例顺序图说明
图书管理员首先获取资源信息以及借书记录，然后读取读者信息，进入归还资源后，增加可借数量，对还书日期登记。查看读者是否逾期还书，若是逾期，进行逾期登记。
***