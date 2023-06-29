# Esp32键盘


<img src="https://github.com/kazawan/notion_note/blob/main/Arduino%20Esp32/Esp32%E9%94%AE%E7%9B%98/B3A1F484-B230-43D2-A1D7-F499F3937CD9.jpeg" width="400px" alt="成品" >

- [x]  按键冲突

      使用keypad.h 中的multiKey 

- [x]  蓝牙连接不稳定
- [x]  按键反馈不够明显
- [x]  按键松动
- [x]  间距太大 经测量是18mm间距 更正：19.05mm
- [x]  4*5 矩阵
- [x]  左上角功能键
    
    使用layerState 状态判断
    
    - [ ]  尝试一下枚举，因为可能会有很多页面
- [ ]  设计外壳
- [ ]  低功耗
- [ ]  Ws2812灯光效果
- [ ]  Webclient 上位机后端改键
- [ ]  Electron vue3前端
- [ ]  震动马达 drv2605
- [ ]  0.91 oled
- [ ]  滚轮编码

pcb高度1.6mm

esp32 高度3.2mm

地板高度2mm

总高度  6.8mm

螺母高度 2.2-2.3mm

1.6 5 2  8.6

## 📒参考

### ⚒️硬件

【【零基础】客制化键盘DIY系列教程（三）如何画出自己键盘的定位板-哔哩哔哩】 [https://b23.tv/QEcCTsh](https://b23.tv/QEcCTsh)

【【机械键盘DIY】真正从零开始 设计制作一款多媒体机械键盘-哔哩哔哩】 [https://b23.tv/xHAkwg](https://b23.tv/xHAkwgm)

【【新手向】自制化键盘第一期——配列/定位板/基础固件-哔哩哔哩】 [https://b23.tv/n3m7tgR](https://b23.tv/n3m7tgR)

### 🍦软件

****《ESP32 学习笔记》 之 ESP32 模拟 蓝牙键盘-Keyboard**** [https://blog.csdn.net/qq_41868901/article/details/106203642](https://blog.csdn.net/qq_41868901/article/details/106203642)

### 🔨键配列网址

[http://www.keyboard-layout-editor.com/#/](http://www.keyboard-layout-editor.com/#/)

### 零件

【淘宝】[https://m.tb.cn/h.UICYr2W?tk=aWokdPLx0HV](https://m.tb.cn/h.UICYr2W?tk=aWokdPLx0HV) CZ3457 「凯华改装机械键盘自主系列插拔轴」

| 类型 | 链接 |
| --- | --- |
| 硬件 |  |
| 客制化键盘DIY系列教程（三）如何画出自己键盘的定位板-哔哩哔哩 | https://b23.tv/QEcCTsh |
| 真正从零开始设计制作一款多媒体机械键盘-哔哩哔哩 | https://b23.tv/xHAkwg |
| 新手向自制化键盘第一期——配列/定位板/基础固件-哔哩哔哩 | https://b23.tv/n3m7tgR |
| 软件 |  |
| 《ESP32 学习笔记》 之 ESP32 模拟 蓝牙键盘-Keyboard | https://blog.csdn.net/qq_41868901/article/details/106203642 |
| 零件 |  |
| CZ3457 「凯华改装机械键盘自主系列插拔轴」 | https://m.tb.cn/h.UICYr2W?tk=aWokdPLx0HV |
| 配置网站 |  |
| 键配列网站 | http://www.keyboard-layout-editor.com/#/ |
| 定位板网站 | http://builder.swillkb.com/ |
| Eda设置网格方法对齐 | https://www.zfrontier.com/app/flow/40KBkWGrmMz3 |
| KEYPAD 多按键同时使用方法 | https://github.com/Chris--A/Keypad/blob/master/examples/MultiKey/MultiKey.ino |
| qmk 矩阵连线方法 | https://kbfirmware.com/ |

键盘连接

```jsx
[
	['fn','*','/','-'],
	['7','8','9','+'],
	['4','5','6'],
	['1','2','3'],
	['0','.','enter'],
]
```

![Untitled](Esp32%E9%94%AE%E7%9B%98%20f032537d01eb4722bc5ad22e6ea5415d/Untitled.png)

### ble_Keyboard 动态检测按键

```jsx
void keypadEvent(KeypadEvent key){
   switch (kpd.getState()){
    case PRESSED:
        break;

    case RELEASED:
        if (key == '1') {
            bleKeyboard.release(KEY_MEDIA_VOLUME_DOWN);
        }
        if(key == '2'){
          bleKeyboard.release(KEY_MEDIA_VOLUME_UP);
        }
        break;

    case HOLD:
        if (key == '1') {
            
            bleKeyboard.press(KEY_MEDIA_VOLUME_DOWN);
        }
        if(key == '2'){
          bleKeyboard.press(KEY_MEDIA_VOLUME_UP);
        }
        break;
    }
}

void setup(){
	kpd.addEventListener(keypadEvent); // add an event listener for this keypad
  kpd.setHoldTime(200); // 设置按键保持时间
  kpd.setDebounceTime(10); // 设置按键去抖时间

}
```

`代码备份`

```jsx
#include <Arduino.h>
// #include <WiFi.h>
// #include <webserver.h>
#include <BleKeyboard.h>

#define led 2
#define key 14
#define CTRL 0x80

// const char *ssid = "K'S_HOME";
// const char *password = "00189423";

// WebServer server(80);

// void handleRoot() {
//   server.send(200, "text/plain", "hello from esp32!");
// }

// void postHandler() {
//   String body = server.arg("plain");
//   Serial.println(body);
//   if (body == "on") {
//     digitalWrite(led, HIGH);
//   } else if (body == "off") {
//     digitalWrite(led, LOW);
//   }
//   server.send(200, "text/plain", "ok");
// }

// String msg = "hello world";
// void keyChange(){
//   String body = server.arg("plain");
//   msg = body;
//   server.send(200, "text/plain", "ok");
// }

BleKeyboard bleKeyboard("ESP32 Keyboard");

void setup()
{
  Serial.begin(115200); // 初始化串口
  pinMode(led, OUTPUT); // 设置led引脚为输出
  pinMode(key, INPUT_PULLUP); // 设置key引脚为输入

  // WiFi.begin(ssid, password);// 连接到WiFi
  // while (WiFi.status() != WL_CONNECTED) {
  //   delay(500);
  //   Serial.println("Connecting to WiFi..");
  // }
  // Serial.println(WiFi.localIP().toString());
  // server.enableCORS();
  bleKeyboard.begin();
}

int lastTime = 0;

// boolean keypress(int *key){

//   if (digitalRead() == LOW) {
//     if (millis() - lastTime > 1000) {
//       lastTime = millis();
//       return true;
//     }
//   }
//   return false;
// }

// boolean blueConnected(){
//   int bluestate = 0;
//   if (bleKeyboard.isConnected()) {
//     if(bluestate == 1 ){
//       Serial.println("connected");
//       bluestate = 0;
//     }

//     return true;
//   }
//   bluestate = 1;
//   return false;
// }

void keyPress(){
  // Serial.println( lastTimes);
  if (digitalRead(key) == LOW)
    {   
      if (millis() - lastTime > 150)
      {
        Serial.println("key pressed");
        bleKeyboard.print("kazawan");
        // todo ctrl+v
        // bleKeyboard.press(CTRL);
        // bleKeyboard.press('v');
        bleKeyboard.releaseAll();
        lastTime = millis();
      }
    }
}

void keyPress2(int *t){
  // Serial.println( lastTimes);
  int tt = *t;
  if (digitalRead(key) == LOW)
    {   
      if (millis() - tt > 150)
      {
        Serial.println("key pressed");
        bleKeyboard.print("kazawan");
        tt = millis();
        *t = tt;
      }
    }
}

void loop()
{
  // 服务器处理客户端请求
  // server.handleClient();

  // if (millis() - lastTime > 1000) {
  if (bleKeyboard.isConnected())
  {
    
    digitalWrite(led, HIGH);
    // if (digitalRead(key) == LOW)
    // {
    //   if (millis() - lastTime > 150)
    //   {
    //     Serial.println("key pressed");
    //     bleKeyboard.print("kazawan");
    //     lastTime = millis();
    //   }
    // }
    // keyPress();
    keyPress2(&lastTime);
    
  }else{
    digitalWrite(led, LOW);
  }
}
```

```
[
    ['esc', 'F1', 'F2', 'F3', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12', 'prt sc', 'scroll lock', 'pause'],
    ['~', '!', '@', '#', '$', '%', '^', '&', '*', '(', ')', '_', '+', 'backspace'],
    ['tab', 'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'I', 'O', 'P', '{', '}', '|', 'delete'],
    ['caps lock', 'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', ':', '"', 'enter'],
    ['shift', 'Z', 'X', 'C', 'V', 'B', 'N', 'M', '<', '>', '?', 'shift'],
    ['ctrl', 'fn', 'alt', 'space', 'alt', 'left', 'down', 'up', 'right', 'ctrl']
]

```

将原来的6行16列键盘调整为8行9列键盘。

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| esc | F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 |
| ~ | ! | @ | # | $ | % | ^ | & | * |
| tab | Q | W | E | R | T | Y | U | I |
| caps lock | A | S | D | F | G | H | J | K |
| shift | Z | X | C | V | B | N | M | del |
| ctrl | alt | space | alt | fn | left | down | up | right |

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| esc |  |  |  |  |  |  |  |  |
| ~ | ! | @ | # | $ | % | ^ | & | * |
| tab | Q | W | E | R | T | Y | U | I |
| caps lock | A | S | D | F | G | H | J | K |
| shift | Z | X | C | V | B | N | M | del |
| ctrl | alt | space | alt | fn | left | down | up | right |

```jsx
[
[]
]
```
