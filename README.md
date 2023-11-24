# Trajectory_car
**Цель работы** - Сборка машинки из предоставленных деталей и создания кода его движения.

## Результат

Движение по квадрату




https://github.com/Alberyn/Trajectory_car/assets/78211591/355dc092-7d3f-4744-8329-8fef3cb437a7




Движение по сердечку

https://github.com/Alberyn/Trajectory_car/assets/78211591/53fa85f7-3abb-46ac-9078-52ce3a27d452

## Сборка бота

![детали](https://github.com/Alberyn/Trajectory_car/assets/78211591/c214ae78-8739-439d-93cf-392cbb5974e4)

Рисунок 1 - Список основных деталей

Список большинства деталей использованных в сборке. Детали напечатанные на 3Д принтере и из фанеры (колеса, стойка) сделанны Дашей и Мадинной.

![сборка](https://github.com/Alberyn/Trajectory_car/assets/78211591/8d62f24e-6bb2-402a-b404-3f5c6bf3df60)

Рисунок 2 - Разнесенные виды бота

![виды](https://github.com/Alberyn/Trajectory_car/assets/78211591/71373b57-95bb-43e8-bcfb-a76229a3c6ff)

Рисунок 3 - Собранный бот

В ходе сборки оказалось, что в платформе не хватает двух отверстий для крепления держателя фломастера, высверливали с помощью шуруповерта.

![впроцессе](https://github.com/Alberyn/Trajectory_car/assets/78211591/5e186ec5-70f4-4716-ae46-81750aa07ca1)

Рисунок 4 - Бот в процессе сборки

Информации, представленной на рисунках 2 и 3, хватает для собственной сборки бота.

## Код движения

Благодаря ранее проведенным парам, код для движения по квадрату и в форме сердечка, мы написали самостоятельно. Начало движения начиналось с нажатия кнопки на пульте управления.

**Траектория квадрата на машинке по команде с пульта**

```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 0
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_CH_PLUS 71
#define IR_BUTTON_CH_MINUS 69
#define IR_BUTTON_PLAY_PAUSE 67

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      if (command = IR_BUTTON_MINUS) {
        
        
        
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 200); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed поехали прямо

          delay(500);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 200); // set speed

          
          delay(500);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 200); // set speed

         

          delay(500);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 200); // set speed

       
          delay(500);


          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);  



          
      }
  }
}
```

**Траектория сердечка на машинке по команде с пульта**

```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 0
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_CH_PLUS 71
#define IR_BUTTON_CH_MINUS 69
#define IR_BUTTON_PLAY_PAUSE 67

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      if (command = IR_BUTTON_MINUS) {
        
        
        
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 200); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed поехали прямо

          delay(500);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 200); // 1 povorot vlevo

          
          delay(800);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 200); // vpered

          delay(400);

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 200); // 1 povorot vpravo

       
          delay(900);

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 200); // vpered
          delay(400);

          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 200); // 2 povorot vlevo

          
          delay(1600);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 200); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed поехали прямо

          delay(1100);




          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);  
          delay (600);



          
      }
  }
}
```

**Примечание**
1) Из-за утягивания ленты соединяющей колеса и общей несовершености конструкции, прямолинейного движения не добиться, бота заворачивает в одну из сторон.
2) Мощность моторчиков питающихся от компьютера и от батареек отличается кардинально, так как тесты на движение бота проводились сначала  без подключенных батареек (чтобы не тратить их заряд), то мощность моторов была минимально и колеса не крутились, из-за чего складывалось представление о неправильности сборки или дефекте деталей. Предлагаю сделать пометку о первоначальной проверке работоспособности сборки и кода с подключенными батарейками.
