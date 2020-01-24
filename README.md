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
1. [Manual](#Manual)
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

 - Updating our code to improve usability. By testing out few programs, we recognized key "SENT" and "DEL" should at first.
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
***Alphabet to binary ver3***
```
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all the letters and digits to the keyboard
String menu0[]={"SENT", "DEL", "SPACE", "NUM", "A-M", "N-Z" };
String menu1[]={"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M"};
String menu2[]={"N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"};
String menu3[]={"0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "!", "?", "&"};

int menuSelected = 0; //by default is the menu1
int numOptions = 6; //size of keyboard


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
  if(menuSelected==0)
  {
    lcd.print(menu1[index]);
  }
  else if (menuSelected==1)
  {
    lcd.print(menu2[index]);
  }
  else if (menuSelected==2)
  {
    lcd.print(menu3[index]);
  }
  
  
  lcd.setCursor(0, 1);
  lcd.print(text);
  delay(100);
}

//This function changes the letter in the keyboard
void selected(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    
 }
}

//this function adds the letter to the text or send the msg
void changeLetter(){
  long last_interrupt_time = 0;
  long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assume
    
   //count number of botton presses
   index++;
   if(menuSelected == 0 && index>6)
   {
      //this makes sures that the index does not go outside the menu1
      index=0;
    }else
    {//any other menu has 13 options
        if(index>13)
        {
          index=0; 
        }  
    String key = menu0[index];
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    else if(key == "SPACE")
    {
      text += " ";
    }
    else if(key == "SENT") 
    {
      text="";
    }
    else if(key == "A-M")
    {
      menu1[]={"A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M"};
    }
    else if(key == "N-Z")
    {
      menu2[]={"N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"};
    }
    else if(key == "NUM")
    {
      menu3[]={"0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "!", "?", "&"};
    }
    index = 0;
    }
  }
}
```

**Binary to Alphabet**
```
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all options to the keyboard
String keyboard[]={"SEND","DEL", "0", "1"};

int numOptions = 4; //size of keyboard

String bin = ""; //where the binary will be stored(input) in string data format

long int todecode; //binary number in int data format

int bidigit; //digit of the binary number

int decimal; //decimal representation of the binary number

int i; //iteration

String text;
// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 5, 4, 9, 8);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  Serial.begin(9600);
  //set interrupts
  attachInterrupt(0, changeLetter, RISING);//button A in port 2
  attachInterrupt(1, selected, RISING);//button B in port 3
}

void loop() {
  
  // (note: line 1 is the second row, since counting begins with 0):
  //clear lcd
  lcd.clear();
  //set the cursor to column 0, line 0 and print keyboard option
  lcd.setCursor(0, 0);
  lcd.print(keyboard[index]);
  //set the cursor to column 6, line 1 and print binary input message
  lcd.setCursor(6, 0);
  lcd.print(bin);
  //set the cursor to column 0, line 1 and print the text converted from binary input 
  lcd.setCursor(0, 1);
  lcd.print(text);
  
  delay(100);
}

//This function changes the keyboard option
void changeLetter(){
  //debouce function
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
 //debounce function
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms
    
    String key = keyboard[index];
    //if DEL is selected, the last character stored in the "bin" variable is deleted
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    //if SENT is selected, the binary is converted to decimal
    else if(key == "SEND")
    {
      todecode = bin.toInt();
      while (todecode > 0) {
        remainder = todecode % 10;
          
        bidigit = decimal + bidigit * ( 0.5 + pow(2,i) );
        
        todecode = todecode / 10;
        i++;
      }
      Serial.println(decimal);
      //The decimal is sent to the bintoeng function
      bintoeng(decimal);
      //the input is set to empty again
      bin = " ";
      //restart all the variables in the conversion process
      decimal=0;
      i=0;
      delay(100); 
    }
    ////if any of the numbers are selected, they are stored to the "bin" variable
    else{
      bin+= key;
    }
    index = 0; //restart the index
  }
  
  
}

//function to convert decimal to character
void bintoeng(int sum){
  //each decimal represent a binary that represents a character
  switch(sum){
  case 1:
    Serial.println("A");
    text += "A";
    break;
  case 2:
    Serial.println("B");
    text += "B";  
    break;
  case 3:
    Serial.println("C");
    text += "C";  
    break;
  case 4:
    Serial.println("D");
    text += "D";
    break;
  case 5:
    Serial.println("E");
    text += "E";  
    break;
  case 6:
    Serial.println("F");
    text += "F"; 
    break;
  case 7:
    Serial.println("G");
    text += "G";
    break;
  case 8:
    Serial.println("H");
    text += "H";  
    break;
  case 9:
    Serial.println("I");
    text += "I";
    break;
  case 10:
    Serial.println("J");
    text += "J"; 
    break;
  case 11:
    Serial.println("K");
    text += "K";
    break;
  case 12:
    Serial.println("L");
    text += "L"; 
    break;
  case 13:
    Serial.println("M");
    text += "M"; 
    break;
  case 14:
    Serial.println("N");
    text += "N";
    break;
  case 15:
    Serial.println("O");
    text += "O";
    break;
  case 16:
    Serial.println("P");
    text += "P";
    break;
  case 17:
    Serial.println("Q");
    text += "Q";
     break;
  case 18:
    Serial.println("R");
    text += "R";
     bin = " ";
    break;
  case 19:
    Serial.println("S");
    text += "S";
    break;
  case 20:
    Serial.println("T");
    text += "T";
    break;
  case 21:
    Serial.println("U");
    text += "U";
    break;
  case 22:
    Serial.println("V");
    text += "V";
     bin = " ";
    break;
  case 23:
    Serial.println("W");
    text += "W"; 
    break;
  case 24:
    Serial.println("X");
    text += "X";
    break;
  case 25:
    Serial.println("Y");
    text += "Y"; 
    break;
  case 26:
    Serial.println("Z");
    text += "Z";
    break;
  case 27:
    Serial.println("1");
    text += "1";
    break;
  case 28:
    Serial.println("2");
    text += "2"; 
    break;
  case 29:
    Serial.println("3");
    text += "3";
    break;
  case 30:
    Serial.println("4");
    text += "4";
    break;
  case 31:
    Serial.println("5");
    text += "5";
    break;
  case 32:
    Serial.println("6");
    text += "6";
    break;
  case 33:
    Serial.println("7");
    text += "7";
    break;
  case 34:
    Serial.println("8");
    text += "8";
    break;
  case 35:
    Serial.println("9");
    text += "9";
    break;
  case 36:
    Serial.println("0");
    text += "0";
    break;
  case 37:
    Serial.println(" ");
    text += " ";
    break;
  }
}
```

**Alphabet to binary final**
```
String engtext= "THIS IS A TEST";
int lightBulb1=6;
int lightBulb2=7;
char toconvert;

void setup()
{
  Serial.begin(9600);
  pinMode(lightBulb1,OUTPUT);
  pinMode(lightBulb2,OUTPUT);
}

void loop()
{
  //separate the message in characters
  for ( int n=0; n < engtext.length(); n++)
  {
   toconvert= engtext.charAt(n);
    Serial.println(toconvert); 
    //send character to engtobin function to convert it to binary
     engTobin(toconvert);
  }
  digitalWrite(lightBulb2, LOW);
  delay(2000);
  digitalWrite(lightBulb1, HIGH);
  digitalWrite(lightBulb2, HIGH);
  delay(100);
  digitalWrite(lightBulb1, LOW);
  digitalWrite(lightBulb2, LOW);
  
  
  while(1)
  {
    //stop loop 
  }
}
//function to convert the character into binary
void engTobin(char x)
{
  switch(toconvert)
  {
    //every character has a binary representation
    case 'A':
      Serial.println("000001");
      binToLightBulb("000001");
      break;
    case 'B':
      Serial.println("000010");
      binToLightBulb("000010");
      break;
    case 'C':
      Serial.println("000011");
      binToLightBulb("000011");
      break;
    case 'D':
      Serial.println("000100");
      binToLightBulb("000100");
      break;
    case 'E':
      Serial.println("000101");
      binToLightBulb("000101");
      break;
    case 'F':
      Serial.println("000110");
      binToLightBulb("000110");
      break;
    case 'G':
      Serial.println("000111");
      binToLightBulb("000111");
      break;
    case 'H':
      Serial.println("001000");
      binToLightBulb("001000");
      break;
    case 'I':
      Serial.println("001001");
      binToLightBulb("001001");
      break;
    case 'J':
      Serial.println("001010");
      binToLightBulb("001010");
      break;
    case 'K':
      Serial.println("001011");
      binToLightBulb("001011");
      break;
    case 'L':
      Serial.println("001100");
      binToLightBulb("001100");
      break;
    case 'M':
      Serial.println("001101");
      binToLightBulb("001101");
      break;
    case 'N':
      Serial.println("001110");
      binToLightBulb("001110");
      break;
    case 'O':
      Serial.println("001111");
      binToLightBulb("001111");
      break;
    case 'P':
      Serial.println("010000");
      binToLightBulb("010000");
      break;
    case 'Q':
      Serial.println("010001");
      binToLightBulb("010001");
      break;
    case 'R':
      Serial.println("010010");
      binToLightBulb("010010");
      break;
    case 'S':
      Serial.println("010011");
      binToLightBulb("010011");
      break;
    case 'T':
      Serial.println("010100");
      binToLightBulb("010100");
      break;
    case 'U':
      Serial.println("010101");
      binToLightBulb("010101");
      break;
    case 'V':
      Serial.println("010110");
      binToLightBulb("000010");
      break;
    case 'W':
      Serial.println("010111");
      binToLightBulb("010111");
      break;
    case 'X':
      Serial.println("011000");
      binToLightBulb("011000");
      break;
    case 'Y':
      Serial.println("011001");
      binToLightBulb("011001");
      break;
     case 'Z':
      Serial.println("011010");
      binToLightBulb("011010");
      break; 
    case '1':
      Serial.println("011011");
      binToLightBulb("011011");
      break;
    case '2':
      Serial.println("011100");
      binToLightBulb("011100");
      break; 
    case '3':
      Serial.println("011101");
      binToLightBulb("011101");
      break; 
    case '4':
      Serial.println("011110");
      binToLightBulb("011110");
      break; 
    case '5':
      Serial.println("011111");
      binToLightBulb("011111");
      break; 
    case '6':
      Serial.println("100000");
      binToLightBulb("100000");
      break;
    case '7':
      Serial.println("100001");
      binToLightBulb("100001");
      break;
    case '8':
      Serial.println("100010");
      binToLightBulb("100010");
      break; 
     case '9':
      Serial.println("100011");
      binToLightBulb("100011");
      break;
     case '0':
      Serial.println("100100");
      binToLightBulb("100100");
      break;
      case ' ':
      Serial.println("100101");
      binToLightBulb("100101");
      break; 
    default:
      digitalWrite(lightBulb1, LOW);
    
    
  }
    
}

//show binary through lamps 
void binToLightBulb(char x[]){
 
  for(int i=0; i < 6;i++){
    //this is the clock, ON
    digitalWrite(lightBulb1,HIGH);
    
    //read one bit of the msg
    char bit = x[i];
    Serial.println(bit);
    
    //when binary equals 0 turn lamp on(buzzers work the opposite way);
    if (bit=='0'){
      digitalWrite(lightBulb2, HIGH);
    }else{
      digitalWrite(lightBulb2, LOW);
    }
    //wait a second
    delay(1000);
    //turn off CLOCK
    digitalWrite(lightBulb1,LOW);
    delay(1000);
  }
  
}
```

**English INPUT**
```
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all the letters and digits to the keyboard
String keyboard[]={"SENT", "DEL", "SPACE", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", };

int numOptions = 39; //size of keyboard

String text = "";//variable to store input


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
  //start lcd
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.clear();
  lcd.setCursor(0, 0);
  //print keyboard option
  lcd.print(keyboard[index]);
  lcd.setCursor(0, 1);
  //print input
  lcd.print(text);
  delay(100);
}

//This function changes the letter in the keyboard
void changeLetter(){
  //debouce button
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms
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
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms
    
    String key = keyboard[index];
    //if DEL is selected, the last character stored in the "text" variable is deleted
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    //if SENT is selected, the "text" variable is emptied
    else if(key == "SENT")
    {
      text="";
    }
    //if SPACE is selected, a space is added to the "text" variable
    else if(key == "SPACE")
    { 
      text += " ";
    }
    //if any othe roption(characters and numbers) are selected, they are stored to the "text" variable
    else{
      text+= key;
    }
    //after any option is selected, the program loops back to the first option
    index = 0; 
  }
  
  
}
```
Manual
-----

**English to binary**
```
This is the manual of how to use our “English to binary” arduino.

This program has 2 input buttons with color blue and red.
With 2 output light that shows binary code.

By pressing the blue button, you can scroll through the options. 
Options are “send” “del” “space” “a” “b”.....”z”
When you accidentally pass through the option you want to select, you have to start the loop again to scroll.

By pressing the red button you can select the options. You cursor is on “send” option and press red button, the program will send the text you inputted.

After you send the text you inputted, the output light will blink. This will show the text you typed in binary code.

One light will blink on a regular basis, this light is used as counter. This will blink to show the knot of the code.

Other light will blink to show the binary code.
For example, “A” is “000001” in binary. This case the light will pause first 5 blink of the counter clock and blink once for the last count.
```

**Binary to English**
```
This is the manual of how to use our “binary to English” arduino.

This program has 2 blue and red input buttons. 
With output LCD screen attached to bread board.

Blue input button is used to scroll down the options. By pressing the button you can go forward to scroll through the options in the program “send” “del” “0” “1”. 

Red button is used to select the options.
By selecting “000001” and press “send” you can express the binary code in to English.

When you miss type your code during the selection, first you have to send the code and delete it to restart typing it.

Ex. You wanted to type “000001” but you missed “001”.  In this case, you have to first “send” the miss typed code. And then press “del” to delete the text.

After sending the binary code, English ver should be shown on to LCD screen. 
So basically after user inputted their code, output should be shown automatically.

Ex. “000001” “send” -> “A”
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
Another class
```
Test 3:
Figuring out circuit's hole.
We reorganized and reprogrammed both our circuit and code to check where the issues are. 
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
