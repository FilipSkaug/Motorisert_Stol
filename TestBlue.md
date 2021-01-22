const int ledPin = 2;
int recived = 0;

void setup() {
  Serial.begin (9600);
  pinMode(ledPin,  OUTPUT);
}

void loop(){
  if(Serial.available() > 0); {
    recived = Serial.read();
  }
  if(recived == 'D'){
    digitalWrite(ledPin, HIGH);
  }
  if(recived == 'd') {
    digitalWrite(ledPin, LOW);
  }
}
