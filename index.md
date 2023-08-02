# Phone Controlled 3 Joint Robotic Arm
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and interest them in what you've built. You can include the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!


```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ajay K | Town School For Boys | Mechanical Engineering | Incoming 8th Grader



![Headstone Image](logo.svg)
  
# Final Milestone

 


# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/hUWw4qFSlUg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For my second milestone, I installed the app to control the arm from my phone and completed the arm. I can now control the arm using the app. In the future, I hope to add several pre-programmed buttons that are set to press specific buttons. Now, when I am upstairs, I can turn my PC or Xbox on with the push of a button.

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/lFjpQyV0S-0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone is using the controller joysticks to output coordinates on the serial monitor. I did this by wiring the joysticks to the Arduino and then adding the code to print out in the serial monitor. Some difficulties that I encountered were putting the wires in the exact pins because it was a really small space, and dealing with some broken parts along the build. 


# Schematics 


# Code
 

```c++
void setup() {#include <Servo.h>  // add the servo libraries
Servo myservo1;  // create servo object to control a servo
Servo myservo2;
Servo myservo3;
Servo myservo4;
int pos1=90, pos2=90, pos3=90, pos4=90;  // define the variable of 4 servo angle and assign the initial value( that is the boot posture angle value)
char val;
int incomingByte = 0;          // Received data byte
String inputString = "";         // Used to store received content
boolean newLineReceived = false; // Previous data end flag
boolean startBit  = false;  //Acceptance Agreement Start Sign
int num_reveice=0;
void setup()
{
   // boot posture
  myservo1.write(pos1);  
  delay(1000);
  myservo2.write(pos2);
  myservo3.write(pos3);
  myservo4.write(pos4);
  delay(1500);

  Serial.begin(9600); //  set the baud rate to 9600
}

void loop() 
{
  myservo1.attach(3);  // set the control pin of servo 1 to D3
  myservo2.attach(5);  // set the control pin of servo 2 to D5
  myservo3.attach(6);   // set the control pin of servo 3 to D6
  myservo4.attach(9);   // set the control pin of servo 4 to D9

while (Serial.available())
  {
    incomingByte = Serial.read();              //One byte by byte, the next sentence is read into a string array to form a completed packet
    if (incomingByte == '%')
    {
      num_reveice = 0;
      startBit = true;
    }
    if (startBit == true)
    {
      num_reveice++;
      inputString += (char) incomingByte;     
    }
    if (startBit == true && incomingByte == '#')
    {
      newLineReceived = true;
      startBit = false;
    }
    
    if(num_reveice >= 20)
    {
      num_reveice = 0;
      startBit = false;
      newLineReceived = false;
      inputString = "";
    }  
  }

if(newLineReceived)
{
    switch(inputString[1])   
    {
      case 'B':  T_left();  break;   // turn left
      case 'C':  T_right();  break;//turn right 
      case 'A':  RB();  break;// the lower arm will draw back 
      case 'D':  RF();  break;// the lower arm will  stretch out
      case '5':  ZK();  break;//close the claw
      case '6':  ZB();  break;//close the claw
      case '4':  LB();  break;//the upper arm will lift up 
      case '7':  LF();  break;//the upper arm will go down 
      default:break;
    }

      inputString = "";   // clear the string
      newLineReceived = false;
}   
     
}
//**************************************************
// turn left
void T_left()
{
    pos1=pos1+8;
    myservo1.write(pos1);
    delay(5);
    if(pos1>180)
    {
      pos1=180;
    }
}
//turn right 
void T_right()
{
    pos1=pos1-8;
    myservo1.write(pos1);
    delay(5);
    if(pos1<1)
    {
      pos1=1;
    }
}
//********************************************
//close the claw

void ZK()
{
      pos4=pos4-8;
      Serial.println(pos4);
      myservo4.write(pos4);
      delay(5);
      if(pos4<45)
      {
        pos4=45;
      }
}
// open the claw
void ZB()
{
    pos4=pos4+8;
      Serial.println(pos4);
      myservo4.write(pos4);
      delay(5);
      if(pos4>120)
      {
        pos4=120;
      }
}

//******************************************
// the lower arm will  stretch out
void RF()
{
    pos2=pos2-8;
    myservo2.write(pos2);
    delay(5);
    if(pos2<25)
    {
      pos2=25;
    }
}
// the lower arm will draw back 
void RB()
{
    pos2=pos2+8;
    myservo2.write(pos2);
    delay(5);
    if(pos2>180)
    {
      pos2=180;
    }
}

//***************************************
//the upper arm will lift up  
void LB()
{
  pos3=pos3+8;
    myservo3.write(pos3);
    delay(5);
    if(pos3>135)
    {
      pos3=135;
    }
}

//the upper arm will go down  

void LF()
{
  pos3=pos3-8;
    myservo3.write(pos3);
    delay(5);
    if(pos3<0)
    {
      pos3=0;
    }
}

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Robot Arm Kit | This is the kit that I used to make the project | $35 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/LAFVIN-Acrylic-Mechanical-Compatible-Tutorial/dp/B07ZYZVNY4/ref=sr_1_6?crid=2SAMMJR9DITS2&keywords=lafvin+robot+arm&qid=1689190533&sprefix=lafvin+rob%2Caps%2C147&sr=8-6)"> Link </a> |


# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
