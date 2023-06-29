# 32u4/pro micro /leonardo 串口坑笔记

### 串口pinout

| 串口 | RX | TX | 可用 |
| --- | --- | --- | --- |
| uart1 | 1 | 0 | 是 |

### 串口使用

注意必须是 `Serial1` ✅

```jsx
Serial1.begin(9600);
```

### 串口发送

```jsx
Serial1.println(foo);
```

### 串口事件 serialEvent1

```参考: [https://github.com/kazawan/arduino_funtion_lib/blob/main/fadercontrol/32U4SIDE](https://github.com/kazawan/arduino_funtion_lib/blob/main/fadercontrol/32U4SIDE)`

[arduino_funtion_lib/32U4SIDE at main · kazawan/arduino_funtion_lib](https://github.com/kazawan/arduino_funtion_lib/blob/main/fadercontrol/32U4SIDE)

注意⚠️

该函数名字大小写必须为这样

`serialEvent1()`  🆙

```jsx
void serialEvent1() //已经在hardwareSerial库里面有定义这个函数了需要主要一下大小写
{
  while (Serial1.available() > 0)
    {
      RXCMD += char(Serial1.read());
      delay(2);
      Serial.println(RXCMD);
      sys_init_flag = 1;
    }
    if (RXCMD.indexOf(cmd_tag) >= 0)
    {
      index = RXCMD.indexOf(cmd_tag);
      flashTime = RXCMD.substring(index+1).toInt();

      Serial1.println("/1"); // send back to confirm 1: init done 0: not init
      sys_init_flag = 1;
      RXCMD = "";
    }
    else
    {
      RXCMD = "";
      Serial1.println("/0"); // send back to confirm
    }
}
```

另外如果使用arduino uno 可以使用 `serialEvent()` 🆙