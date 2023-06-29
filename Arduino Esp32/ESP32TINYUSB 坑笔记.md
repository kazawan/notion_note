# ESP32TINYUSB 坑笔记

库地址

[GitHub - chegewara/EspTinyUSB: ESP32S2 native USB library. Implemented few common classes, like MIDI, CDC, HID or DFU (update).](https://github.com/chegewara/EspTinyUSB)

platformio 库名叫 `ESP32TinyUSB` 不是esptinyusb 

### 坑💩

[MIDI Not working · Issue #52 · chegewara/EspTinyUSB](https://github.com/chegewara/EspTinyUSB/issues/52)

\ESP32TinyUSB\src\device\midi\midiusb.cpp

头文件下 `EPUNM_MIDI`  由 `0x05` 改成 `0x04`

## ESP32 USBMIDI使用

```jsx
#include "midiusb.h"

MIDIusb espmidi;

//setup
espmidi.begin("ESP Native MIDI");

//loop

///按键
espmidi.noteON(70, 127);//note value
espmidi.noteOFF(70, 0);

//推子
espmidi.controlChange(38, val); //cc value

```

## ESP32 USBKEYBOARD使用

键盘表在`\.pio\libdeps\esp32-s3-devkitc-1\ESP32TinyUSB\src`

```jsx
#include "hidkeyboard.h"

HIDkeyboard dev;

//setup
dev.begin();

//loop
dev.sendKey(0x2c, KEY_SHIFT); keycode 在上面地址

```