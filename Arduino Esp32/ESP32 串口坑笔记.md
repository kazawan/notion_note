# ESP32 串口坑笔记

## 硬串口

下表列出了 ESP32 中可用的三个 UART 端口的 RX 和 TX 引脚。

| 串口 | RX管脚 | TX管脚 | 使用情况 |
| --- | --- | --- | --- |
| uart0 | 3 | 1 | 不使用 |
| uart1 | 9 | 10 | 使用需要重新定义管脚 |
| uart2 | 16 | 17 | 可以使用 |

### 使用uart2

```jsx
#include <HardwareSerial.h>

HardwareSerial espSerial(2); // RX 16, TX 17
espSerial.begin(9600);
```

### 发送

```jsx
espSerial.println(TxMsg);
```

### RX任务中断

`参考 https://github.com/kazawan/arduino_funtion_lib/blob/main/fadercontrol/ESP32SIDE`

[arduino_funtion_lib/ESP32SIDE at main · kazawan/arduino_funtion_lib](https://github.com/kazawan/arduino_funtion_lib/blob/main/fadercontrol/ESP32SIDE)

```jsx
espSerial.onReceive(RxTask);//setup中使用
```

```jsx
void RxTask() // 中断出发回调函数
{

  String msg = "";
  while (espSerial.available() > 0)
  {
    RxMsg += char(espSerial.read());
    delay(2);
  }
  if (RxMsg.indexOf(cmd_tag) >= 0)
  {
    tag_index = RxMsg.indexOf(cmd_tag);
    sys_init_flag = RxMsg.substring(tag_index + 1).toInt();
    RxMsg = "";
  }
  else
  {
    RxMsg = "";
  }
}
```