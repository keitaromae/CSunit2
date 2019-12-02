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
1. [Development](#Development)
1. [Project](#Project)
1. [References](#References)

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

This is the program that convert alphabet, numbers into binary and send or delete by using 2 button inputs.
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


Project
-----
**//Plan (defining the problem)**

**//Solution proposed**

**//Success criteria**

**//About**

Build a communication method from Earth to Mars. 
 - Earth to Moon (Alphabet to Morse)
 - Moon to Mars (Morse to Binary)

They have different outputs between each stars, so the program between them would be very crucial.

**//Tasks:**
 - Enter English text show in the serial monitor use the LED screen.

Moon to Mars (Morse to Binary)
```
Input = 2 buttons
but A, Selects the alphabet
but B, All the options (Ent, space, Del and Send)


Output = Alphabet in Binary
```

**//Evaluation**


References
-----

[1] Wikipedia "Usability." Wikipedia, 13 November 2019
https://en.wikipedia.org/wiki/Usability

[2] Whitney Quesenbery "What is usability." WQusability, 2001
http://www.wqusability.com/articles/more-than-ease-of-use.html

[3] Arduino "Volatile." Arduino, 2019
https://www.arduino.cc/en/pmwiki.php?n=Reference/Volatile
