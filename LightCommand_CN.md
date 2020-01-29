# Light Commands：基于激光的音频攻击在声控系统中的应用Test
---
作者：
 - Takeshi Sugawara（日本电气通信大学）邮箱：sugawara@uec.ac.jp
 - Benjamin Cyr（美国密歇根大学）邮箱：bencyr@umich.edu
 - Sara Rampazzi（美国密歇根大学）邮箱：srampazz@umich.edu
 - Daniel Genkin（美国密歇根大学）邮箱：genkin@umich.edu
 - Kevin Fu（美国密歇根大学）邮箱：kevinfu@umich.edu

译者：
 - bleach103  [github](https://github.com/bleach103)
 - 777024     [github](https://github.com/777024)

---
## 摘要
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本论文提出了一种应用于麦克风的新型信号注入攻击手段，该手段基于光声效应（[photoacoustic effect](https://en.wikipedia.org/wiki/Photoacoustic_effect)）同过使用麦克风将激光转换成声音。本文将展示一个攻击者如何通过使用被调幅调制（[amplitude-modulated](https://en.wikipedia.org/wiki/Amplitude_modulation)）过的激光射向麦克风的小孔，将任意一段音频信号注入目标麦克风的过程。此后将继续展示这种效应如何被应用于声控系统的远程注入攻击中
## 介绍
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;持续增长的计算机算力正在深远的改变着人和计算机互相影响的方式。除去像鼠标和键盘一样的传统输入方式，在最近几年里，计算机已经变得足够强大去理解和处理人类所说的话。一些认识到这种快速，自然的人机交互潜力的科技巨头，像苹果，Google，Facebook，和亚马逊都相继开始大规模部署他们各自的可持续听和反应人类语言指令的语言控制系统。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;随着以千万计的像Alexa，Siri，Portal和Google Assistant这样的硬件发售，用户现在可以不坐在电脑前，也不用在智能电话上打字，就和服务供应商进行交互。为了回应这种趋势，物联网(IoT)市场也经历了一场小型革命。比起每个设备都有专用的软件，物联网(IoT)制造商现在会在制造一些硬件，并给这些硬件上提供一个轻量型的接口用于向Alexa，Siri或者Google Assistant整合上花更多时间。因此，用户仅仅通过说话就可以收到信息和控制产品， 不需要和键盘，鼠标，触摸屏，甚至按钮进行交互。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;然而，当聚光灯都照在提高VC(voice-controllable)系统的能力上时，我们就会更少得知这些系统在软件和硬件攻击上的顺应性。甚至，之前的工作[1, 2]已经标记出了只有语音交互的主要限制：缺少可靠的用户认证。同样的，语音控制系统也可以在没有额外的用户认证的情况下执行注入命令。当早期命令注入方式被设备的合法拥有者轻易的注意到了之后，最近的工作[3, 4, 5, 6, 7, 8, 9]更加专注于隐秘的命令注入，防止用户识别，甚至是听到注入命令。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这些对语音认证的忽视导致了一个基于附近的威胁模型，当附近的用户被认为是合法的时候。当攻击者被物理阻碍像墙，锁住的门或者关上的窗户锁在外面时。对攻击者来说，他们要找到一种隐蔽的方式去控制物理上难达到的系统，现存的指令注入方式显然受到限制，正如文章[6]的状态所述，它有着在开阔空间只有25$ft$(7.62 m)，有物理格挡(e.g. 窗户)则会大大减少的距离限制。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;因此，在本篇论文里我们主要处理以下问题：命令能被悄悄地远程注入到一个语音控制系统里吗？如果能，攻击者如何能在被物理限制的现实条件里施展攻击？最后，对这些命令注入到语音控制的第三方物联网(IoT)设备这件事儿有什么启示？
