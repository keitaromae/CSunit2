# CSunit2

contents
-----
1. [Reflection](#Reflection)
1. [Development](#Development)
  
  
  
Reflection
-----


Development
-----
**how to count in binary?***
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
