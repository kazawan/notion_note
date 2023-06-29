# ESP32-S3 USB   串口坑

```jsx
#include <Arduino.h>
#include "esp32-hal-log.h"
#include "esp_log.h"

#define led 48

void setup()
{
  Serial.begin(115200);
  Serial.println("Starting"); // will be shown in the terminal
  Serial.setDebugOutput(true);

  
  pinMode(led, OUTPUT);
}

void loop()
{
  digitalWrite(led, HIGH);
  log_i("ledpin: %d", digitalRead(led));
  delay(1000);
  digitalWrite(led, LOW);
  log_i("ledpin: %d", digitalRead(led));
  delay(1000);
  Serial.printf("Hello World\n");
  
 
}
```

后补

## 使用s3 usb口串口 ini设置

```jsx
build_flags =
   -DARDUINO_USB_MODE=1
   -DARDUINO_USB_CDC_ON_BOOT=1
monitor_port = /dev/cu.usbmodem14*
monitor_speed = 115200
monitor_rts = 0
monitor_dtr = 0
```