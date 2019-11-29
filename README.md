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

**What is USABILITY??**

 - In software engineering, usability is the degree to which a software can be used by specified consumers to achieve quantified objectives with effectiveness, efficiency, and satisfaction in a quantified context of use.
Any discussion of usability must include the idea of ergonomics and accessibility [1].

 - "The extent to which a product can be used by specified users to achieve specified goals with effectiveness, efficiency, and satisfaction in a specified context of use”[2]
 

Project
-----
**Plan (defining the problem)**

**Solution proposed**

**Success criteria**

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
```

**Evaluation**


References
-----

[1] Wikipedia "Usability." Wikipedia, 13 November 2019
https://en.wikipedia.org/wiki/Usability

[2] Whitney Quesenbery "What is usability." WQusability, 2001
http://www.wqusability.com/articles/more-than-ease-of-use.html
