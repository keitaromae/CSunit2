# CSunit2

Table of contents
-----
1. [Development](#Development)
1. [Usability](#Usability)
1. [Project](#Project)

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

Usability
-----
**What is USABILITY??**

 - In software engineering, usability is the degree to which a software can be used by specified consumers to achieve quantified objectives with effectiveness, efficiency, and satisfaction in a quantified context of use.
Any discussion of usability must include the idea of ergonomics and accessibility [1].

 - "The extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency, and satisfaction in a specified context of use”[2]
 
**Resources**

[1] https://en.wikipedia.org/wiki/Usability

[2] http://www.wqusability.com/articles/more-than-ease-of-use.html

Project
-----
**About**

Build a communication method from Earth to Mars. 
 - Earth to Moon (Alphabet to Morse)
 - Moon to Mars (Morse to Binary)

They have different outputs between each stars, so the program between them would be very crucial.

**Tasks:**
 - Enter English text show in the serial monitor use the LED screen.

Moon to Mars (Morse to Binary)
```
Input = 2 buttons
but A, Selects the alphabet
but B, All the options (Ent, space, Del and Send)


Output = Alphabet in Binary
Input


