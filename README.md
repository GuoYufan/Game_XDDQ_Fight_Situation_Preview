# -
目前准备完成两个项目：《寻道大千战况预览》《寻道大千挑选对手》
// updated：？~2025.1.11 16:08
《寻道大千战况计算器C语言代码v1.0.1（尝试修复了部分问题）》

《v1.0.1版本概要》
从尝试解决上一版本的遗留问题——蚀魂咒问题——入手。
成功模拟了一场打1.6倍有必复活（扶桑+煌气免疫冰冻所以必然复活）有治疗（煌气）有锁血（金刚不坏）的对手，战况准度极高。
并且在这场通过使赌可赌的运气强制为不需要赌快速（不需要运行那么多次）复现了与实战中完全相同的100%胜率方法。

《尝试修复了部分问题》
一、蚀魂咒的问题
蚀魂咒在普攻前触发，使得蚀魂咒出现在掉血回妖气之前，那么蚀魂咒就阻止不了对手回满妖气了。
而如果放到普攻之后出发，由于蚀魂咒内开头写了一句逻辑“当对方复活未起身则不触发蚀魂咒”。使得如果本次普攻属于“补刀”，对手被标记为“复活未起身”，代码认为复活未起身的目标不应被触发蚀魂咒。使得掉血回妖气，然后进入复活未起身。如果掉血回满妖气，那么复活起身时就是满妖气，因为蚀魂咒未发挥作用。而事实上蚀魂咒应当发挥作用。
最新版本使用了这样的解决办法：即便目标被标记为“复活未起身”，仍然对其施放蚀魂咒。因为妖气这800是必扣的。你到了10000妖气，然后复活未起身，不可能让你起身时是10000。而是你起身时必须是9200。
正是由于蚀魂咒问题，造成打那个1.6倍对手模拟出的战况准度太差，毫无价值。

《增加支持情况》
一、增加支持的神通
驭兽神通(5+1)：煌气。

二、增加支持的精怪
减伤类(1+1)：大山妖。
战斗属性类(1)：大明王。

三、增加对灵兽的支持的情况
1.支持效果：青龙的战斗属性之暴击加成。
2.支持协同灵兽的行动。

四、增加对人物的支持情况
支持暴击与抗暴。
支持百分百闪避（不支持概率闪避）。

五、增加对战况操控的支持情况
（战况操控通常用于把“可赌的部分”变成“不需要赌”，也就是“强制”。）

1.赌必暴。
自己.战斗属性之暴击+=(100-(自己.战斗属性之暴击-对手.战斗抗性之抗暴))。

2.赌对手的协同灵兽永不行动。
对手.协同灵兽出手概率=0。

3.赌我方的协同灵兽行动多少次。（比如用于补伤害。）
我方.协同灵兽出手概率=0。
对手.已损生命+=0.0374252*1。
（其中第一个乘数为伤害，第二个乘数为强制协同灵兽行动多少次。）


// updated: 2024.6.29 20:17 ~ 2024.7.2 5:11

《寻道大千战况计算器C语言代码v1.0.0（第一个可用版本）》


《目前支持情况》

一、目前支持的神通
驭兽神通(5)：碎心法/共鸣/丹心同并/回春/暗袭。
被动神通(7)：化羽/铜皮铁骨/金刚不坏/飘渺身/长生体/兽灵体/大魔邪身。
神识神通(5)：识海钉/拘神/附灵术/蚀魂咒/啮心吞灵。
道法神通：伤害部分及治疗部分全部支持。
效果部分几乎都不支持。
对效果部分支持的道法神通有：七十二变/冰封千里。


二、目前支持的精怪
复活类(1)：扶桑。
减伤类(1)：小龙女。
强灵类(2)：大树妖/马面。
治疗类(2)：山泽精/干饭人。
无视防御伤类(3)：雷公/紫晴龙狮/皇帝。
基础属性类(2)：破阵书生/玄冥蛟。
增伤类(2)：鬼将/骨魅。


三、目前对灵兽的支持情况
1.只支持百分比攻击力伤害与百分比攻击力治疗。
不支持任何效果（如计蒙的弱疗、朱雀的延长晕回合、青龙的加战斗属性之暴击）。

2.不支持协同灵兽的行动。


四、目前对人物的支持情况
战斗属性及战斗抗性只支持一种：击晕与抗晕。
暂不支持：暴击与抗暴、连击与抗连、反击与抗反、闪避与抗闪、吸血与抗吸。

五、目前对强化弱化的支持情况
支持：增伤系数/强灵系数。
不支持：强疗系数。


六、友好使用支持
支持随时切换任意灵兽流。
不用每次在<void 当前对手()>函数中手动修改。
而是在<void Fight_info_init()>函数中添加灵兽流即可。



七、目前对战况操控的支持情况
1.支持通过增加漏晕次数来达到无晕。
其实就是全程漏晕。把漏晕次数设置为已知回合数（比如如果发生8回合，则可以设置10）以上。
建议设置为20以上，因为一般最多也就15回合。

2.支持设置稳晕（全程不漏晕）。
如果只是把漏晕次数设置为0，则并不能稳晕。因为击晕率上限为80%。
方法是把漏晕次数设置为0，同时把「除了设置漏晕以外的皆必晕」设置为true。



《使用方法》
一、在同目录下的文件<XDDQ_Fight_Info_Operate.h>里的
void Fight_info_init(Fight_info * self, char *who)
函数里切换哪一组PK双方参赛。
（可写出多组不同的PK双方放在其中，通过注释的取消与否切换哪一组PK双方进行参赛。）

二、在同目录下的文件<XDDQ_双方初始信息.h>中的
void 当前对手(Fight_info *self, char *who)
函数里调整某一组PK双方的信息。

三、主文件（主函数main函数在内）就是同目录下的文件<寻道大千_战况预览.c>。
在编译器里编译后运行即可。


《使用时可能存在的问题》
一、使用时如果（只输出了一部分内容甚至完全没有输出之后）出现Segmentation fault，
重新反复多次编译并运行即可。
