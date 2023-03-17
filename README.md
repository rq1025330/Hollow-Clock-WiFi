# Hollow-Clock-WiFi

3D打印悬浮时钟  
> 声明
该项目原作者为[shiura](https://www.youtube.com/@shiura/about)创作的作品[Hollow-Clock-4](https://www.instructables.com/Hollow-Clock-4/)  
**本项目基于原作的 CC-BY-NC-SA 4.0 协议 在原项目基础上做出改进，不用做商业用途，仅供学习参考使用**
***
不得感叹原作本人的脑洞，原版的时钟是作为单机版本的装饰时钟，存有一定时间误差，且其底座结构窄，很难塞下主板以及驱动板，在此基础上，做了一些改进:  
- 加强其实用性，增添esp8266 nodemcu wifi模块，获取网络时间自主校时，第一次使用时需要校准调整，也可以通过模块内置网页调整时间
- 对其底座结构优化，能塞下wifi主板，驱动板
- 对其外壳增加时间刻度，便于查看时间
***
- 该项目没有整合led灯带，喜欢的光污染的朋友可以自行diy  
- 该项目没有采用电池供电方案，因为电机功耗较大，18650锂电池大约维持50~80h
***
![图片展示](./Docs/Images/wificlock1.PNG)
***
## 项目文件说明

- 3D-model  
3d stl 模型文件
> 预览链接[https://a360.co/3JyfEzB](https://a360.co/3JyfEzB)
- Docs  
相关的耗材清单，参考文件，图片等

| 耗材名称          | 规格/型号    | 数量          | 其他 |
| ----------------- | ------------ | ------------ | ---- |
| 铷磁铁            | 8x3mm        | 3            |      |
| 步进电机          | 28BYJ-48     | 1            |      |
| 电机驱动板        | ULN2003      | 1            | 绿板     |
| 自攻螺丝          | M2(6mm,10mm) | 6mm:7,10mm:1 | 4mm可替代6mm   |
| esp8266           | cp2102驱动   | 1            | 注意尺寸大小，有的板子过大，无法放入底座    |
| 线材              | \            | \            |      |

- Codes  
该目录下为arduino程序  
——time_correction为误差校准程序  
——wifi_main_program为主程序，需要安装三个库文件  
`#include<ESP8266WiFi.h>`  
`#include<NTPClient.h>`  
`#include<WiFiUdp.h>`  
***
## 使用说明
1. 接线说明，程序中`int port[4] = { 15, 13, 12, 14 };`对应8266引脚如下图，分别对应ULN2003驱动板`IN1,IN2,IN3,IN4`

![图片展示](./Docs/Images/esp8266.png)

2. 第一次使用请先烧录该代码`time_corrections`，并将分针和时针指向12点位置，该程序会执行12次校准，最终回到12点位置，通过最后的误差角度，调整主程序代码中STEPS_PER_ROTATION的数值来进行校准`STEPS_PER_ROTATION = 30720 +- 偏差值`
3. 安装好库文件后，需要将主程序内的`INPUT_YOUR_WIFI_ID`，`INPUT_YOUR_WIFI_PASSWORD`修改为自己的WiFi名和密码，烧录后重新上电，等待连接wifi，指针会自动走向当前时间

## License
This project is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/).
