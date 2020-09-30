# self-balsncing-robot
/*
This project aims to build a self-balancing robot that will transform from three wheels to two wheels
This is the code to control the rising movement of the third wheels of the robot by using two servo motor
*/


#include <Servo.h>

Servo myservo_13;
int buttonPin_1 = 8;          // choose the input pin (for a pushbutton)
int buttonPin_2 = 7;
int buttonState_1 = 0;
int buttonState_2 = 0;
int angle = 0;
int angle_step = 10;

void setup(){
 myservo_13.attach(13);
 pinMode(buttonPin_1, INPUT_PULLUP);
 pinMode(buttonPin_2, INPUT_PULLUP);
 myservo_13.write(angle);
}


void loop(){
  buttonState_1 = digitalRead(buttonPin_1);
  buttonState_2 = digitalRead(buttonPin_2);

  
  if(buttonState_1 == LOW){
    if (angle >= 0 && angle <= 90) {
      angle = angle + angle_step;
      if(angle >90){
        angle =90;
       }else{
      myservo_13.write(angle);           // move the servo to desired angle
       }
     } 
       delay(100); 
   }
    

  if (buttonState_2 == LOW){
  
    if (angle >= 0 && angle <= 90) {
      angle = angle - angle_step;
       if(angle < 0){
        angle = 0;
       }else{
      myservo_13.write(angle);                    // move the servo to desired angle
       }
  }else{
  myservo_13.write(angle);
  delay(100);                                                    // waits for the servo to get there
  }
  }
}
