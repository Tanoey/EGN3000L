
# EGN3000L Object Seeking Robot
This code was created for usage in the final project for EGN3000L. The code was created using Arduino, and requires:
- a chassis
- one Arduino Uno
- one ultrasonic sensor
- one H-bridge
- two DC motors and wheels 
- one 9V battery and a connector
- many wires
- A computer and cable to upload code


## Authors

- Patrick Tanoeyjaya (coder)

Other Team Members: Robert Geer, Isaiah Looby, Devanshi Pande, Saksham Srivastava


## Code:

----------------------------------------------------------------


/*
PKT
This is variable declaration. 
You can change the values depending on where you decided to wire, or you can follow what I've set up here
*/
const int trigPin = 7; //the two ultrasonic pins 
const int echoPin = 6;
const int in1 = 4; //the four wheels down here
const int in2 = 5;
const int in3 = 9;
const int in4 = 10;


void setup() {

  Serial.begin(9600); //open serial monitor

  pinMode(trigPin, OUTPUT); //set trigpin to output
  pinMode(echoPin, INPUT); //set echopin to input

  pinMode(in1, OUTPUT); //set all four wheels as output
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);

}

void loop() {
  // put your main code here, to run repeatedly:

  // generate 10-microsecond pulse to TRIG pin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // measure duration of pulse from ECHO pin
  long duration = pulseIn(echoPin, HIGH);
  // calculate the distance
  long distance = 0.017 * duration;// Speed of sound wave, 0.034m/us divided by 2

  // print the value to Serial Monitor. for testing funcitonality
  Serial.print("distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  //check distances, goes in loop function​
  if (distance <= 5) { //check distance is less than 5 cm
  // robot will back up
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);

  } else if (distance <= 10) { //check distance to be 5 - 10 cm
    //robot will be stationary
    digitalWrite(in1, LOW);
    digitalWrite(in2, LOW);
    digitalWrite(in3, LOW);
    digitalWrite(in4, LOW);

  } else if (distance <= 40) {//check distance to be 10 - 40 cm
    //robot will go forwards
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);
    digitalWrite(in3, LOW);
    digitalWrite(in4, HIGH);

  } else { // check distance to be 40+ cm
    //robot will spin and search for target
    digitalWrite(in1, LOW); 
    digitalWrite(in2, HIGH);
    digitalWrite(in3, HIGH);
    digitalWrite(in4, LOW);

  }

}
