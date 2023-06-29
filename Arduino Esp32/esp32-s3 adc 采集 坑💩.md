# esp32-s3 adc 采集 坑💩

[GitHub - HwzLoveDz/ESP32-ADC-sense-battery-voltage: The battery voltage is sensed using the ADC pin of the ESP32 and calibrated by averaging filtering and software（超详细注释，ADC电压检测）](https://github.com/HwzLoveDz/ESP32-ADC-sense-battery-voltage/tree/main)

```jsx
//include 两个头文件
#include <driver/adc.h>
#include "esp_adc_cal.h"

#define ADC_CHANNEL ADC1_CHANNEL_3 //点击ADC1_CHANNEL_3 可以查询可以用的ADC 通道
#define ADC_ATTEN_DB ADC_ATTEN_DB_11
#define ADC_WIDTH_BIT ADC_WIDTH_BIT_12

//读取
uint32_t adc_read_val()
{

  int samplingFrequency = 200; // 采样频率（可调）
  long sum = 0;                // 采样和
  float samples = 0.0;         // 采样平均值

  for (int i = 0; i < samplingFrequency; i++)
  {
    sum += adc1_get_raw(ADC_CHANNEL); // Take an ADC1 reading from a single channel.
                                      //
  }
  samples = sum / (float)samplingFrequency;

  // uint32_t voltage = esp_adc_cal_raw_to_voltage(samples, adcChar); // 2.调用 API 函数将 ADC 值转换为电压（在调用此函数之前，必须初始化特征结构，也就是步骤 1）
  // uint32_t voltage = (samples * 2.6) / 4096.0; //通过公式转换为电压

  return samples; // 单位(mV)
}

//xtask任务

void midifaderTask(void *p)
{
  Serial.println("fader task created");
  // fader.prv_value = adc_read_val();
  while (1)
  {
    fader.temp = adc_read_val();
    fader.value = map(fader.temp, 0, 4095, 0, 127);
    if (fader.value - fader.prv_value > 1 || fader.value - fader.prv_value < -1)
    {
      fader.prv_value = fader.value;
      Serial.print("fader val: nowval ---> ");
      Serial.println(fader.value);
    }
  }
}

```

未完