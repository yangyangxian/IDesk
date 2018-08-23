## 游戏
### 关于笔记本测试游戏性能的必要性
对于台式机，给定的显卡型号，比如`GTX1050`，它的性能表现基本就是确定了的。网上测试数据不胜枚举，结合自己需求，参考测试结果购买即可。

但是笔记本则不然，由于散热的限制，笔记本通常会为了防止GPU温度过高，会在GPU温度达到特定温度时降低GPU运行频率。这个温度一般被称为“温度墙”。

所以，即便采用同一个型号的显卡，不同笔记本降频的策略不同，性能表现也会大相径庭。

比如我测试过我媳妇的`惠普Envy13`，机器到手后开玩PUBG，开最低特效，帧数竟然只有个位数，游戏变成PPT。`Envy13`有独立显卡`MX150`，好歹算是入门级里不错的显卡，为何表现比核显还差？我用软件查看GPU运行详情发现，GPU最高温度被限制在68度，而这个时候GPU核心实际运行频率仅为300Mhz！这还能用？我足足研究了一个下午，终于通过升级电脑固件并且调整BIOS里的GPU运行模式，最终让GPU运行的温度锁定在72度，运行频率900Mhz。虽然仍处于略微的降频状态，但是吃鸡也有30来帧了，应急短时间游戏算是可以了。

这就是典型的因为散热的限制，GPU在达到温度墙以后，软件层面对于GPU运行频率进行大幅降低，从而机器的GPU性能大大降低。每个品牌每个机型的GPU运行策略或者BUG都可能不一样，在购买之前，一款笔记本实际的GPU性能表现可能像个迷一样。当然这是对于轻薄本而言，游戏本散热相对足够，一般足以让中低端显卡全速运行。

### Surface Book2 GTX1050
`Surface book 2`作为一款兼顾轻薄的笔记本，游戏性能也值得实际测试一番。

配备独显`GTX 1050`的参数。

<img src="https://github.com/yangyangxian/IDesk/blob/master/Articles/surface%20book2%20gaming%20testing/images/SB2-GPUZ.PNG" alt="GTX-1050" width="50%">

核心频率1354，显存频率1752。显存2GB。
我们最需要关注的是，游戏在运行一段时间之后，GPU的频率是否会低于这个频率，以及会低多少。

**一些测试条件**
* 笔记本插电，并且直接放在桌上，没有垫高。
* 所有游戏帧率采集均在游戏连续运行`20分钟`之后。
* 电源模式：`最佳性能`。经多个游戏实际测试，电源模式对于GPU运行策略影响极大，如果电源模式设置为`更好的性能`，风扇声音小很多，同时，GPU温度也更低，运行频率显著降频，性能大幅下降。所以这里目前只测试`最佳性能`下的表现。

### PUBG
* 测试日期:`2018-08-12`
* 测试室温:`28度`左右
* 游戏分辨率`1920*1200`。PUBG并不支持3:2的分辨率，所以只能调到一个最接近3:2的分辨率，此时游戏画面的拉伸较小。
* 画面质量设置：低。

<img src="https://github.com/yangyangxian/IDesk/blob/master/Articles/surface%20book2%20gaming%20testing/images/Settings.jpg" alt="Settings" width="100%">

**测试结果**

记录游戏5分钟帧数。从跳伞后开始记录帧数。可以看到落地后帧数稳定在50-60fps。

<img src="https://github.com/yangyangxian/IDesk/raw/master/Articles/surface%20book2%20gaming%20testing/images/PUBG-Frames.png" alt="PUBG-Frames" width="80%">

GPU-Z的显卡运行状态：

<img src="https://github.com/yangyangxian/IDesk/blob/master/Articles/surface%20book2%20gaming%20testing/images/PUBG-GPUZ.PNG" alt="PUBG-GPU status" width="50%">

显卡核心频率运行在1400MHz-1500MHz，温度60-65徘徊。极偶尔频率能到1600MHz以上，温度会上升到70度。

核心频率全程稳定运行在Boost频率上下。在温度不超过65度的情况下，GPU能连续满速不降频运行，Surface Book2的GPU部分散热比较不错。

并且Surface的CPU和GPU是分离设计，键盘部分仅有GPU，散热压力相比一般笔记本会小一些。况且GPU本身温度不高，键盘表面只有不常触及的中部上方温热，日常使用起来基本没有任何温度的感觉，体验很好。这算是`Surface Book2`CPU和GPU分离设计的一个优势了吧。不过屏幕部分十分热，有些烫手。


