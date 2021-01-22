const int analogInPin = A0; //Potmeter
const int analogOutPin = 9; //Led

int sensorValue = 0;        //pot
int outputValue = 0;        // value output to the PWM (analog out)

void setup() {

  Serial.begin(9600);
}

void loop() {
  sensorValue = analogRead(analogInPin);
  outputValue = map(sensorValue, 0, 1023, 0, 255);
  analogWrite(analogOutPin, outputValue);
  Serial.print("sensor = ");
  Serial.print(sensorValue);
  Serial.print("\t output = ");
  Serial.println(outputValue);
  delay(2);
}
