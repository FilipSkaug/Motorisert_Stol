const int signalMotorL = 8; //signalpin til venstre motor
const int signalMotorR = 9; //signalpin til høyre motor

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

    int val,cnt=0,v[4];
    int val1,val2,val3,val4;
    int Ok1=1,Ok2=1;
    int delayy2,delayx1,delayy1;


    void readbt() {
        val=Serial.read();
        cnt++;
        v[cnt]=val;
        if(v[1]==1 && cnt==3) {
          cnt=0;
        }
        if(v[1]!=1 && cnt==2) {
          cnt=0;
        }
    }

    void program() {
      timer1++;
      timer2++;
      timer3++;
    }

    TimedAction readbtThread = TimedAction(10,readbt);
    TimedAction timerThread = TimedAction(1,program);

    void setup() {
      // put your setup code here, to run once:
      Serial.begin(9600);
    }

    void loop() {
      // put your main code here, to run repeatedly:
      if(Serial.available()) {
          while(Serial.available() == 0);
          readbtThread.check();
          timerThread.check();
          if(v[1]==1) {
            Ok1=0;
            val1=v[2];
            val2=v[3];
          }
          if(v[1]==2) {
            Ok2=0;
            val3=v[2];
          }
          if(v[1]==3) {
            Ok3=0;
            val4=v[2];
          }
      }
      joystick1();
      joystick2();
      slider();
    }

    void joystick1() {
      if (Ok1==0) {
        timerThread.check();
        if(v[1]==1 && (v[2]==100 && v[3]==100)) {
          Ok1=1;
        }
        if(val1>100) {
          delayx1=((200-val1))+15;
          if(timer1>=delayx1) {
          }
        }
        if(val1<100 && pos1>0) {
          delayx1=val1+15;
          if(timer1>=delayx1) {
            pos1--;
            myservo1.write(pos1);
            timer1=0;
          }
        }
        if(val2>100 && pos2<180) {
          delayy1=((200-val2))+15;
          if(timer2>=delayy1) {
            pos2++;
            myservo2.write(pos2);
            timer2=0;
          }
        }
        if(val2<100 && pos2>0) {
          delayy1=val2+15;
          if(timer2>=delayy1) {
            pos2--;
            myservo2.write(pos2);
            timer2=0;
          }
        }
      }
    }

    void slider() {
      if(Ok2==0) {
        if(pos4==val4) Ok3=1;
        if (val4>pos4) {
          for(int i=pos4;i<=val4;i++) {
            myservo4.write(i);
            delay(15);
          }
        }
        if(val4<pos4) {
          for(int i=pos4;i>=val4;i--) {
            myservo4.write(i);
            delay(15);
          }
        }
        pos4=val4;
      }
    }
    https://create.arduino.cc/projecthub/anova9347/control-your-robot-with-your-phone-joysticks-app-a4ab50
