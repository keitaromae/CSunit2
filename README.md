Feedback Nov 26 (You can deleted this section later. It will remain in the history of the file)

|No.|How to improve        |
|-|------------- |
|①| Start working on the definition of the problem and the proposed solution. You will then add the success criteria based on the planet where you will be working.　This is Criterion A. To define the client you can invent a ficticious person/organization.  | 
|②| Keep adding pictures, small parts of code, sketches, flow diagrams to your development section. Keep the journal only for reflection which answer the questions: What did we do today in class? What did you learn? to do list.|
|③|　Add your References at the bottom of the page using MLA format. I have added the section for you to fill in.|

----

# CSunit2

Table of contents
-----
1. [Planning](#Planning)
1. [Development](#Development)
1. [Evaluation](#Evaluation)
1. [References](#References)


Planning
-----
### Defining the problem

We are creating the communication tool that goes through Moon and Mars.
Very first step sending messages from our planet Earth to the Moon, we suppose that we are not allowed to send messages to Mars directly due to its technical difficulties. Going through Moon is the absolute condition.
Also each planet or star has its own ways of transpassing data. Between Earth and Moon we use morse code, from Moon to Mars,
we use binary code to send data.
By creating useful communication tool, we have to create several programs that convert the inputted data into their readable format. For example, Alphabet to morse code.

### Solution proposed

Using Arduino Uno, 2 button input program to create communication tools that convert several inputs to different format.
Also we are creating this program for each and every people. So the user don't have to know what binary is and how to write in morse. All of the converting process will be done through our program and user only have to input what they want to send.

### Success criteria

These are measurable outcomes

1. Simple usage.
1. User can send their messages without having any extra knowledge.
1. User can write their messages only by using 2 button inputs.
1. Program can convert original data into whatever the format that should be outputted.


### About

Build a communication method from Earth to Mars. 
 - Earth to Moon (Alphabet to Morse)
 - Moon to Mars (Morse to Binary)

They have different outputs between each stars, so the program between them would be very crucial.

### Tasks:

 - Enter English text show in the serial monitor use the LED screen.

Moon to Mars (Morse to Binary)
```
Input = 2 buttons
but A, Selects the alphabet
but B, All the options (Ent, space, Del and Send)


Output = Alphabet in Binary
or
Output = Morse to Binary (work in progress)
```

Development
-----
**how to count in binary?**
 - How to count a number from 0-15 by using arduino
 - Showing numbers in binary form
```
int firstLED = 4;
int secondLED = 8;
int thirdLED = 10;
int forthLED = 13;

byte count;

void setup()
{
  pinMode(firstLED, OUTPUT);
}

void loop()
{
  for (int count=0; count<15; count++);
  
  //firstLED
  if (count%2 == 1) {
    digitalWrite(firstLED, HIGH);
      
  } else {
    digitalWrite(firstLED, LOW);
  }
  
  
  //secondLED
  if (count%4 > 1) {
    digitalWrite(secondLED, HIGH);
    
  } else {
    digitalWrite(secondLED, LOW);
  }
  
  
  //thirdLED
  if (count%8 > 4) {
    digitalWrite(thirdLED, HIGH);
  } else {
    digitalWrite(thirdLED, LOW);
  }
  
  //forthLED
  if (count%16 > 8) {
    digitalWrite(forthLED, HIGH);
  } else {
    digitalWrite(forthLED, LOW);
  }
  delay(200);
}
```

**What is the volatile data type in arduino?**

volatile is a keyword known as a variable qualifier, it is usually used before the datatype of a variable, to modify the way in which the compiler and subsequent program treats the variable.

Declaring a variable volatile is a directive to the compiler. The compiler is software which translates your C/C++ code into the machine code, which are the real instructions for the Atmega chip in the Arduino.

Specifically, it directs the compiler to load the variable from RAM and not from a storage register, which is a temporary memory location where program variables are stored and manipulated. Under certain conditions, the value for a variable stored in registers can be inaccurate.

A variable should be declared volatile whenever its value can be changed by something beyond the control of the code section in which it appears, such as a concurrently executing thread. In the Arduino, the only place that this is likely to occur is in sections of code associated with interrupts, called an interrupt service routine.[3]


**What is USABILITY??**

 - In software engineering, usability is the degree to which a software can be used by specified consumers to achieve quantified objectives with effectiveness, efficiency, and satisfaction in a quantified context of use.
Any discussion of usability must include the idea of ergonomics and accessibility [1].

 - "The extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency, and satisfaction in a specified context of use”[2]
 
***Alphabet to binary program***

 - This is the program that convert alphabet, numbers into binary and send or delete by using 2 button inputs.
```
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all the letters and digits to the keyboard
String keyboard[]={"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "SENT", "DEL"};

int numOptions = 64; //size of keyboard

String text = "";


// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 9, 8);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  attachInterrupt(0, changeLetter, RISING);//button A in port 2
  attachInterrupt(1, selected, RISING);//button B in port 3
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print(keyboard[index]);
  lcd.setCursor(0, 1);
  lcd.print(text);
  delay(100);
}

//This function changes the letter in the keyboard
void changeLetter(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    index++;
      //check for the max row number
    if(index==numOptions){
      index=0; //loop back to first row
    } 
 }
}

//this function adds the letter to the text or send the msg
void selected(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    
    String key = keyboard[index];
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    else if(key == "SENT")
    {
      text="";
    }else{
      text += key;
    }
    index = 0; //restart the index
  }
  //
}
```
![arduino](IMG_0313.jpg)
**First Prototype** (development work in progress)

![arduino2](IMG_0313.jpg)
**code on my PC** (development work in progress)

***since this photo is not shown in markdown, original files are in "Arduino" file in my repository**

***Alphabet to binary ver2***
Updating our code to improve usability. By testing out few programs, we recognized key "SENT" and "DEL" should at first.
So we moved those 2 keys infront of the row and also added "SPACE" key by simply binding " " to its key.
```
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all the letters and digits to the keyboard
String keyboard[]={"SENT", "DEL", "SPACE", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", };

int numOptions = 65; //size of keyboard

String text = "";


// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 9, 8);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  attachInterrupt(0, changeLetter, RISING);//button A in port 2
  attachInterrupt(1, selected, RISING);//button B in port 3
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print(keyboard[index]);
  lcd.setCursor(0, 1);
  lcd.print(text);
  delay(100);
}

//This function changes the letter in the keyboard
void changeLetter(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    index++;
      //check for the max row number
    if(index==numOptions){
      index=0; //loop back to first row
    } 
 }
}

//this function adds the letter to the text or send the msg
void selected(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    
    String key = keyboard[index];
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    else if(key == "SENT")
    {
      text="";
    }
    else if(key == "SPACE")
    { 
      text += " ";
    }
    else{
      text+= key;
    }
    index = 0; //restart the index
  }
  
  
  //
}
```

Evaluation
-----

At this point entire program is not done yet. We need to add up some programs to transmit data from Earth to Moon. Since I was responsible for Moon to Mars section, we have to add each ideas to create one system.
Overall in Moon to Mars section Alphabet to Binary program worked fine without having any errors.
```
Test 1: 
Running "Alphabet to Binary" program by using Arduino
In my team we separated parts into several section. People who build the circuit and people who actually writes the code.
I did the coding part and other did the circuit section. After working on our own parts, we gather up and tested the progress.
First of all we connected our made circuit into my PC and run code throughout Arduino.
For our first try, it didn't work. Alphabets and numbers should appear on our LCD but it didn't show anything.
```
We had to figure it out the cause of an error. Whether it's code or the circuit or even both of them.
```
Test 2:
Running "Alphabet to Binary" program(exactly same code that we used in test1) by using Arduino.
This time we used the original sample circuit that is made by Dr Ruben to see my code is correct or not.
As a matter of fact, it start showing alphabets, numbers and send, del keys. Code did work, so the problem was the circuit it self.
We double checked our circuit and we supposed that there is something wrong with few of the cable ports. Since we didn't have enough time to work on it, we're still not able to create our own circuit yet.
```

**Checking success criteria (Project is not fully done yet)**

1. **Simple usage.**
It is quite simple and easy for user to use but it takes a lot of time to send full sentences.

1. **User can send their messages without having any extra knowledge.**
User just need their necessary Alphabet knowledge. Other work will be 100% done by program.

1. **User can write their messages only by using 2 button inputs.**
Yes, butA for the scrolling and butB to select.

1. **Program can convert original data into whatever the format that should be outputted.**
We have created only "Alphabet to Binary" code, this section will be updated as soon as we created new program.

**Summary**

*Project is not fully done yet*

References
-----

[1] Wikipedia "Usability." Wikipedia, 13 November 2019
https://en.wikipedia.org/wiki/Usability

[2] Whitney Quesenbery "What is usability." WQusability, 2001
http://www.wqusability.com/articles/more-than-ease-of-use.html

[3] Arduino "Volatile." Arduino, 2019
https://www.arduino.cc/en/pmwiki.php?n=Reference/Volatile
