# -
目前准备完成两个项目：《寻道大千战况预览》《寻道大千挑选对手》

// updated: 2024.6.29 20:17 ~ 2024.7.2 5:11

《寻道大千战况计算器C语言代码最新版本之第一个可用版本》


《目前支持情况》

一、目前支持的神通
驭兽神通(5)：碎心法/共鸣/丹心同并/回春/暗袭。
被动神通(7)：化羽/铜皮铁骨/金刚不坏/飘渺身/长生体/兽灵体/大魔邪身。
神识神通(5)：识海钉/拘神/附灵术/蚀魂咒/啮心吞灵。
道法神通：伤害部分及治疗部分全部支持。
效果部分几乎都不支持。
对效果部分支持的道法神通有：七十二变/冰封千里。


二、目前支持的精怪
复活类：扶桑。
减伤类：小龙女。
强灵类：大树妖/马面。
治疗类：山泽精/干饭人。
无视防御伤类：雷公/紫晴龙狮/皇帝。
基础属性类：破阵书生/玄冥蛟。
增伤类：鬼将/骨魅。


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
函数里设置对手。

二、在同目录下的文件<XDDQ_双方初始信息.h>中的
void 当前对手(Fight_info *self, char *who)
函数里调整对手信息。

三、主文件（主函数main函数在内）就是同目录下的文件<寻道大千_战况预览.c>。
在编译器里编译后运行即可。


《使用时可能存在的问题》
一、使用时如果（只输出了一部分内容甚至完全没有输出之后）出现Segmentation fault，
重新反复多次编译并运行即可。
