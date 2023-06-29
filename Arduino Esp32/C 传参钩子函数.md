# C 传参钩子函数

```jsx
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

keyPress2(&lastTime);
```