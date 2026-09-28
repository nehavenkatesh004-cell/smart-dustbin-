# smart-dustbin-
#include <Servo.h>

Servo dustbinServo;

const int moisturePin = A0;
const int servoPin = 9;

// Adjust after testing your sensor
const int wetThreshold = 500;

const int centerPosition = 90;
const int wetPosition = 30;
const int dryPosition = 150;

void setup() {
  Serial.begin(9600);

  dustbinServo.attach(servoPin);
  dustbinServo.write(centerPosition);

  Serial.println("Smart Dustbin Started");
}

void loop() {
  int moistureValue = analogRead(moisturePin);

  Serial.print("Moisture Value: ");
  Serial.println(moistureValue);

  if (moistureValue < wetThreshold) {
    Serial.println("Wet Waste Detected");

    dustbinServo.write(wetPosition);
    delay(2000);
  } 
  else {
    Serial.println("Dry Waste Detected");

    dustbinServo.write(dryPosition);
    delay(2000);
  }

  // Return flap to center
  dustbinServo.write(centerPosition);
  delay(1000);
}
