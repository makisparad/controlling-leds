int inputPins[5] = {2, 3, 4, 5, 6};     // create an array of pins for switch inputs
int ledPins[5] = {9, 10, 11, 12, 13};   // create array of output pins for LEDs
int ledState[5];                         // create array for current led state
int prevLedState[5];                     //create array for previous led state

void setup()
{
  Serial.begin(9600);                     // intiallize serial monitor for monitoring purposes
  
  for (int i = 0; i < 5; i++)
  {
    pinMode(ledPins[i], OUTPUT);        // declare LED as output
    pinMode(inputPins[i], INPUT);       // declare pushbutton as input
    digitalWrite(inputPins[i], HIGH);   // enable pull-up resistors
    digitalWrite(ledState[i], 0);
    digitalWrite(prevLedState[i], 0);
  }
}

void loop() 
{
  Serial.println(" -----------------------------------------------");
  for (int i = 0; i < 5; i++)
  { 
    ledState[i] = 1 - digitalRead(inputPins[i]);            // not pushing button gives 0 state
    Serial.print(" Button : ");  Serial.print(i);    
    Serial.print(" Led is : ");  
    if (ledState[i] == 1) 
    {
      Serial.print("ON ");
    }
    else
        {
         Serial.print("OFF "); 
        }
    prevLedState[i] = ledState[i];
    Serial.print(" Led was : "); Serial.print(prevLedState[i]);
    Serial.println(""); 
    delay(400);
    if (prevLedState[i] == 1) 
    {
      digitalWrite(ledPins[i], 1);
    }
    else{}
    int val = digitalRead(inputPins[i]);                         // read input value
    
    if (val == LOW)                                            // check if the switch is pressed
    {
      digitalWrite(ledPins[i], HIGH);                         // turn LED on if switch is pressed
    }
   else
   {
      digitalWrite(ledPins[i], LOW);                          // turn LED off      
    }
  }
}
