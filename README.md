# blowing_smoke_rings
Using a microphone to sense a human "blow" that triggers a solenoid to "hit". This set-up was used in our case to hit the membrane of a chamber filled with smoke, which resulted in smoke rings!

int soundDetectedPin = A0; // Use Pin A0 as the Input (Microphone sensor)
int soundDetectedVal = HIGH; //
boolean bAlarm = false; // Either false or true (it has two variable values)
int solenoidPin = 6; // Use Pin 6 as our Output (Solenoid)

void setup ()
{
  Serial.begin(9600); // Data rate in bits per second for serial data transmission to computor
  pinMode (A0, INPUT_PULLUP) ; // Input from the Sound Detection Module, "pullup" in pin A0 is activated
  pinMode(solenoidPin, OUTPUT); // Output from solonoid (pin 6)
}

void loop ()
{
  soundDetectedVal = digitalRead(A0); // Read the sound value
  Serial.println(soundDetectedVal);
  if (soundDetectedVal == LOW) //If we hear a sound
  {
    Serial.println(bAlarm);
    if (!bAlarm) {
      Serial.println("LOUD, LOUD");
      digitalWrite(solenoidPin, HIGH); //Switches Solenoid ON
      delay(500); //Delay provides correct time that the Solenoid hits the membrane
      bAlarm = true;
    }
 }
  else
  
  {
    Serial.println("QUIET");
    bAlarm = false;
    digitalWrite(solenoidPin, LOW);
    digitalWrite(solenoidPin, LOW); //Switches Solenoid OFF
    //delay(400); //Sensor experiences no delay to have a more accurate reaction time
  }

}

Code sources: 
http://henrysbench.capnfatz.com/henrys-bench/arduino-sensors-and-input/arduino-sound-detection-sensor-tutorial-and-user-manual/
https://www.bc-robotics.com/tutorials/controlling-a-solenoid-valve-with-arduino/ (by Chris @ BCR, July 2015)


