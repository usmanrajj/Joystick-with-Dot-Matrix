/*
Rajj YT
Video Link :-
https://youtu.be/vZNOckwU4ag

Circuit :-
https://github.com/usmanrajj/Joystick-with-Dot-Matrix

Library Link :-
https://github.com/nfhktwrbq/LedMatrix8x8
*/
#include "LedControl.h"

// Pin definitions for the joystick
int JOYSTICK_X = A0;
int JOYSTICK_Y = A1;
int DIN=7;
int CLK=5;
int CS=6;

// Create an instance of the LedControl library
LedControl lc=LedControl(DIN,CLK,CS,1); //Din,CLK,CS,Module number 1

void setup() {
  lc.shutdown(0,false); // Wake up the dot matrix
  lc.setIntensity(0,8); // Set the brightness of the dot matrix
  lc.clearDisplay(0);  // Clear the dot matrix
}

void loop() {
  int xVal = analogRead(JOYSTICK_X); // Read the X-axis value of the joystick
  int yVal = analogRead(JOYSTICK_Y); // Read the Y-axis value of the joystick
  lc.clearDisplay(0);
  // Map the joystick values to coordinates on the dot matrix
  int x = map(xVal, 0, 1023, 0, 7);
  int y = map(yVal, 0, 1023, 0, 7);
  lc.setLed(0,x,y,true); // Turn on the LED at the joystick coordinates
}
