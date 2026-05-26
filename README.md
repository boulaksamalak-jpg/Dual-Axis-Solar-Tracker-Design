/*
  Dual-Axis Solar Tracker with Arduino UNO
  Author: Malak BOULAKSA
  Project: Solar Tracker (Suiveur Solaire)
  Institution: Badji Mokhtar - Annaba University, Algeria
  License: MIT
*/

#include <Servo.h>

// LDR analog pins
const int ldrTopLeft = A0;
const int ldrTopRight = A1;
const int ldrBottomLeft = A2;
const int ldrBottomRight = A3;

// Servo objects
Servo servoHorizontal;
Servo servoVertical;

// Initial servo positions (center: 90°)
int posHorizontal = 90;
int posVertical = 90;

// Movement limits (0° to 180°)
const int LIMIT_MAX = 170;
const int LIMIT_MIN = 10;

// Delays (microseconds)
const int DELAY_SHORT = 8;
const int DELAY_MEDIUM = 50;

void setup() {
  Serial.begin(9600);
  
  servoHorizontal.attach(9);   // Horizontal servo (East-West)
  servoVertical.attach(10);     // Vertical servo (Tilt)
  
  servoHorizontal.write(posHorizontal);
  servoVertical.write(posVertical);
  
  delay(1000);  // Wait for servos to stabilize
}

void loop() {
  // Read LDR values (0-1023)
  int valTL = analogRead(ldrTopLeft);
  int valTR = analogRead(ldrTopRight);
  int valBL = analogRead(ldrBottomLeft);
  int valBR = analogRead(ldrBottomRight);
  
  // Calculate averages
  int avgTop = (valTL + valTR) / 2;
  int avgBottom = (valBL + valBR) / 2;
  int avgLeft = (valTL + valBL) / 2;
  int avgRight = (valTR + valBR) / 2;
  
  // === Vertical control (Up/Down) ===
  int verticalDiff = avgTop - avgBottom;
  
  if (abs(verticalDiff) > 20) {  // Threshold to avoid jitter
    if (avgTop > avgBottom) {
      // Move UP
      if (posVertical > LIMIT_MIN) {
        posVertical--;
        servoVertical.write(posVertical);
        delayMicroseconds(DELAY_SHORT);
      }
    } 
    else {
      // Move DOWN
      if (posVertical < LIMIT_MAX) {
        posVertical++;
        servoVertical.write(posVertical);
        delayMicroseconds(DELAY_SHORT);
      }
    }
  }
  
  // === Horizontal control (Left/Right) ===
  int horizontalDiff = avgRight - avgLeft;
  
  if (abs(horizontalDiff) > 20) {
    if (avgRight > avgLeft) {
      // Move RIGHT
      if (posHorizontal < LIMIT_MAX) {
        posHorizontal++;
        servoHorizontal.write(posHorizontal);
        delayMicroseconds(DELAY_SHORT);
      }
    } 
    else {
      // Move LEFT
      if (posHorizontal > LIMIT_MIN) {
        posHorizontal--;
        servoHorizontal.write(posHorizontal);
        delayMicroseconds(DELAY_SHORT);
      }
    }
  }
  
  // Serial monitor output (optional, for debugging)
  Serial.print("H:");
  Serial.print(posHorizontal);
  Serial.print(" V:");
  Serial.print(posVertical);
  Serial.print(" | Diff H:");
  Serial.print(horizontalDiff);
  Serial.print(" Diff V:");
  Serial.println(verticalDiff);
  
  delayMicroseconds(DELAY_MEDIUM);
}
