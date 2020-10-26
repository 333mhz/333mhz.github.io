## 游星异想 | Aether Daze
游戏设计文档 | Game Design Document  
版本0.1 | Version 0.1
Atelier17th/Pixel kaleido

### 简介
> 1.指挥部队与来自气星深处的外星怪物战斗
2.运营浮空小镇，维持部队开支
3.探索这颗气态行星

### 介绍　|　Intro/Statement  
> 游戏名称：游星异想
Game Name：Aether Daze  
游戏类型：图像冒险+ATB策略扮演+模拟经营 
Game Type：AVG+SRPG+SIM
平台：Win10 NWJS
Platform：PC x86 Win10 NWJS 
目标人群：大于12岁的男性群体 
Target Market：Males，age 12+    
竞品：未调查  
Competitive Product: Unknown  
目标定价：36 RMB  
Target Price: 5 Dollars  
难度等级：简单到困难  
Difficult Level: Easy to Very Hard  
关卡数量：三大章节，每章附数小节  
Number of Level: (undefine)  
游戏时间：8-15小时  
Hours of Play Value: 8-15  
暴力等级：中度  
Violence Level: Mild --> Very Violent  
> 图形重点：2d.pixel,
> 1.角色为平面2D纸片人，SPINE 2D动画
> 2.地图为正面透视方块构成（类似明日方舟的战斗地图场景）追求素材的重复利用最大化。
>   
Graphics Emphasis:  
---
> 主要角色：  
1.玩家（自定义驾驶员）  
2.尤利欧（灵能男孩）   
3.杰利（士兵男孩）  
4.桐夏（怪物女孩）  
Main Character:   
Player(customize pilot),   
Yurio(Psi Boy),  
Jelly(Soldier Boy),  
TongXia(Monster Girl)  
---
>　额外注释：无
Additional Note: None

ATB-SRPG指加入了ATB队列的策略角色扮演游戏

1.地图，跟传统SRRG一样，平面走格子。
（参考wargrove、sd gundam g generation和super robot battle，）
2.角色行动的方式，是按一个时间队列依次进入不同角色行动回合，总体有大回合控制；
 ( 参考Tactics_Orge-皇家骑士团2 WildArm、空之轨迹）
3.行动大致分为三种，1不加延迟的行动，2稍加延迟的行动，3队列延迟极大的行动

4.角色的移动、技能，释放都有行动范围。
（类似lol、dota2）
5.角色的被动、攻击方式和技能都是独特的.
（类似lol、dota2）


创新点：
1.在SRPG大地图基础上改善普通回合制表现力不足和过于公式化的感官感受
2.通过时间队列改善SLG内回合制必须我动敌动的特点，增加爽快感，变相降低难度
3.技能机制和装备，改变传统RPG技能过于公式化的问题，同时使同一角色在不同装备下拥有不同玩法。

目前思路
每次我方行动都暂停给指令

地图
单位-角色
单位-装置
技能
装备

初代地图，跟传统SLG一样，平面走格子。（方便做，成本低）
未来地图希望3D化，角色移动坐标化

单位基本数值

HP-HealthPoint：生命值-绿
- 生命值高低会影响攻击能力和行动速度
- 生命值在战场上通常难以恢复
ARP-ArmorPoint：护甲值-白
- 可道具按数值恢复
- 按照数值减少伤害
SHP-SheildPoint：护盾值-蓝
- 按数值恢复
- 每层降低伤害

ATK-Attack：角色基础攻击属性

ATP：    基础行动速度
（初期思路（DelayTimeSum/SPD*TechnicalModulus) = DelayTime）
MOV-Mobility:     基础移动能力

<!-- ORDO:    传统RPG属性的命中暴抗成分将被统一成秩序值。
（此外，秩序值跟一些技能有关联性）
PERDITIO:传统RPG属性的暴击回避成分将被统一成混乱值。
（此外，混乱值跟一些技能有关联性） -->

<!-- //Dex 命中值
//AGL回避值
//Critical 暴击值
//Anti Critical 暴抗值 -->
double DamageEfficiency

乘于物理系数/能量/热/灵能等
<!-- ORDO：角色秩序能力
（例如：物理系ordo值高）    
PERDITIO：角色混乱能力
（例如：能量系perditio值高）
Re-ORDO类型
（例如：物防系reordo值高）
Re-PERDITIO类型
（例如：能防系reperditio值高） -->

技能基本属性

伤害属性-DamageType
斩（线-斩断）Fracture - 对护盾1.0对护甲1.0对生命2.0
刺（点-刺穿）Puncture - 对护盾1.0对护甲2.0对生命1.0
崩（面-崩裂）Rupture  - 对护盾2.0对护甲1.0对生命1.0

例:
1.武器-匕首 攻击范围一格 斩系数0.5刺系数0.5 对护盾x1.0对护甲x1.5对生命x1.5
1.武器-长刀 攻击范围一格+ 斩系数0.8刺系数0.2 对护盾x1.0对护甲x1.2对生命x1.8
1.武器-手枪 攻击范围三格 刺系数0.7崩系数0.3 对护盾x1.3对护甲x1.7对生命x1.0
<!-- 属性系数-DamageModulus（0.0-2.0）
分5个等级。
Thermal    热系数（炙热寒冰）——无视一半护甲，依次对护甲和生命造成损伤。同时可赋予持续伤害debuff。存在护甲时，debuff真伤比例低。
正值为提供一个过热的debuff，可叠加，层数越高，debuff伤害量越高，每次伤害消耗一层。
负值为提供一个冰冻的debuff，可累计，叠5层，降低敌人行动速度，回避率。

Electron    电系数（电子微观）——无视一半护甲，依次对护盾和生命造成损伤。同时赋予伤害debuff。存在护盾时，debuff真伤比例低。
正值为提供一个过载的debuff，叠满封锁敌人技能。
负值为提供一个削弱的debuff，根据层数降低敌人伤害效率。

Light         光系数（电磁辐射）——无视护甲，同时对护盾和生命造成损伤。
正值为提高集束攻击距离和降低衰减量。
负值为提高辐射攻击范围和降低衰减量。

Cosmos    暗系数（引力空间）——无视护盾、同时对护甲和生命造成损伤。
正值为空间压缩，使处于该格的单位可移动距离减少。
负值为空间扩张，使处于该格的单位受到的伤害增加。 -->

伤害公式：

int    SP;//护盾值
int    AP;//护甲值
int    HP;//生命值

int    TotalDamage;//对生命值伤害
int    ShieldDamage;//对护盾伤害
int    ArmorDamage;//对护甲
int    OverDamage;//护甲护盾受到的溢出伤害
int    TrueDamage;
double DamageEfficiency;//攻击效率，受多种因素影响。
int    DebuffDamage

HP -= TotalDamage;

TotalDamage =    TrueDamage    +    OverDamage + DebuffDamage;

TrueDamage =    ATK*(P+S+B)*(L+C+T+E)*DamageEfficiency;

ShieldDamage = ATK*(P/2+B)*(E+L)*DamageEfficiency;
ArmorDamage = ATK*(P/2+S)*(E+L)*DamageEfficiency;
SP =(    (SP>ShieldDamage)?(SP-ShieldDamage):0);
AP =(    (AP>ArmorDamage)?(SP-ArmorDamage):0);
OverDamage =    ((SP>ShieldDamage)? 0 : ShieldDamage)+((AP>ArmorDamage)? 0 : ArmorDamage);

DebuffDamage;

概述
---------------------------
在一个行动队列上，不分敌我依次行动。
每场战斗最多可以指挥1-N个小队，在地图上行动。
采用和少女前线类似的小队战斗的方式。
每个小队有五个行动单位。

界面要素-地图指挥
----------------------------
1大地图-地形
2行动队列
3行动小队-我方
3-1小队行动选项：
3-2战斗（当敌我小队接触时）、
3-3移动、
3-4MAP技能(地图技能）、
3-5强制脱离
4行动小队-敌方
5状态文字显示栏（log）
6按钮-退出场景-1.不结束战斗退出 2.结束战斗并退出 3.重开作战
7按钮-战斗信息显示

界面要素-小队战斗
----------------------------
1地图-根据大地图生成的地形
2行动队列
3行动单位-我
4行动单位-敌
5状态文字显示栏（log）
6按钮-退出战斗-强制退出？小队将从战场上撤离

3-1选择单位行动方式
3-2攻击/防御（将姿态调整为攻击态势并结束回合、主动选择攻击对象）
3-2-1这里的攻击不同于传统RPG或SLG中普攻，
3-2-2是指持续的对攻击范围内的选定单位进行攻击
3-2-3攻击取决于按攻击方式（高射速远程可以每次队列都平A一次）
3-3防御/回避/反击（将姿态调整为防御态势/回避态势/反击态势并结束回合）
3-4技能（通常为3个技能和一个大招、有的角色能切换技能组，使用技能并结束回合，有的技能不结束本回合）
3-5道具（使用道具并结束回合）
3-6避战（类同RPG中逃跑，可能结束，可能无法结束并消耗该角色回合）

概述
战场行动按小队指挥
小队战斗以单位操作

小队
每支小队可最多编成6个单位
其中4个为目前战斗单位，2个后备（被偷袭时会打乱顺序）
每个小队都有一个COST值，
COST值决定小队每次出击的资源消耗值
此外COST有上限，
部分精英单位可能一个单位就消耗完小队所有的cost

单位
兵-Pawn-兵-P
相-Guard-御-G

马-Knight-骑-N
炮-Musket-铳-S

车-Automata-傀-A
士-Wizard-术-W

王/后-King/Queen-皇-K/Q





