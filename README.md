# DIY-Arduino-based-Wire-harness-wrapping-Machine

![image](https://user-images.githubusercontent.com/19898602/188255610-5b2b3769-ecd0-4425-b6fe-db2494329058.png)


Hello friends in this post I have build a Arduino based wire harness wrapping machine.

some time wrapping tape to wire harness is very challenging and time consuming job
so made this simple machine to minimize the work and we can quickly wrap the tape
to wire harness.

# Component Used

1. Arduino nano

2. A4988 stepper driver

3. Custom PCB

4. Limit switch

5. 12mm wooden sheet

6. 6mm acrylic

7. Some hardware

8. wrapping tape

![image](https://user-images.githubusercontent.com/19898602/188255630-348e5dd0-6ee2-490a-bd96-195511f9fc00.png)![image](https://user-images.githubusercontent.com/19898602/188255633-c6e1b0e3-e537-431b-ac19-69dfb542c5b4.png)


To make the base of this machine I have used 12mm wooden sheet.

I cut the base of size 150 x 220 mm , I used my mini table saw to cut the wooden sheet
and I used my bench sander to sand the edges of the wooden sheet.

![image](https://user-images.githubusercontent.com/19898602/188255638-0df60138-4fea-48b1-9e5a-672f9278cb27.png)![image](https://user-images.githubusercontent.com/19898602/188255641-325790ca-44ef-4c1b-8120-30683352f2b4.png)![image](https://user-images.githubusercontent.com/19898602/188255642-87eed409-86af-48fd-a9df-51afee8aa99b.png)



After completing the base of the machine now I have made the C shape acrylic part.
this ring is made from 6mm acrylic sheet, I have cut the shape by using my home made CNC router machine.

This ring circle around the wire and tape is attached to this ring.


![image](https://user-images.githubusercontent.com/19898602/188255656-ff67c8bd-e368-4d14-bab6-83df55d3e606.png)![image](https://user-images.githubusercontent.com/19898602/188255660-8ceefad3-8627-4fbc-a035-d6d5fb938172.png)![image](https://user-images.githubusercontent.com/19898602/188255662-ca9326f0-ce49-4072-94c2-71760f351ee2.png)


Then I print a templet on plain white paper, and pasted on the wooden sheet and cut the outline using my jigsaw machine.

![image](https://user-images.githubusercontent.com/19898602/188255674-bb719607-6e11-4e63-9a3c-575b397fa7b6.png)

The I place the acrylic ring inside the roller so it will rotate sooty.



![image](https://user-images.githubusercontent.com/19898602/185791830-840591de-59d2-4163-9a0c-d918fba861c4.png)

![image](https://user-images.githubusercontent.com/19898602/188255679-9cf2987a-edb0-4536-a118-c69dc9db21b1.png)


For this project I have used my multipurpose PCB this PCB can be used for so many projects. 

I have design circuit and PCB in easyEDA and ordered PCB from [JLCPCB](https://jlcpcb.com/IAT )


[JLCPCB](https://jlcpcb.com/IAT ) are the world leader in PCB manufacturing there PCB production rates are very much affordable and they have world class PCB production unit results fast PCB production.

I have provided the link of circuit design so that you can modify it as per your need if you need to change anything.

[Multipurpose custom PCB](https://oshwlab.com/sharmaz747/multipurpose-pcb_copy_copy_copy)




This is the custom made PCB used in this project. by the way this is multipurpose PCB it can be used for wide range of arduino project.

If you are interested to order this PCB so you can find the Gerber file of the PCB here

[Multipurpose custom PCB](https://oshwlab.com/sharmaz747/multipurpose-pcb_copy_copy_copy)


![image](https://user-images.githubusercontent.com/19898602/188255753-78070b6b-d726-4cac-8e2e-b27034581e03.png)

I have 3D printed the circular part to hold the wrapping tape
also I have used a spring to make tension on the tape so that wrapping tape release with tension
and wrap over wire tightly.


![image](https://user-images.githubusercontent.com/19898602/188255759-ad4af777-646c-49f8-80a9-7c5b7d028117.png)

Here I have used a limit switch with a long notch.
This limit switch is used to start and stop the wrapping.
When we first press the limit switch it will start winding and when we press it again
it will stop the winding.

# Arduino Code

````
#include <Arduino.h>
#include "BasicStepperDriver.h"
#define MOTOR_STEPS 200
#define RPM 500
boolean A = 0;
int flag = 0;
int val = 0;
#define MICROSTEPS 8

#define DIR A2
#define STEP A3
int state = 0;
BasicStepperDriver stepper(MOTOR_STEPS, DIR, STEP);


void setup() {
    stepper.begin(RPM, MICROSTEPS);
    pinMode(9,INPUT_PULLUP);
}

void loop() {
A = digitalRead(9);
  Serial.println(A);
if (A==1 && flag==0 && state == 0){
  flag = 1;  
}
if (A==1 && flag == 1 && state == 1){
  flag = 0;
  delay(1000);
  state = 0;
}
if (flag==1 && A==0){
  stepper.rotate(3414);
  state = 1;
}}

````


