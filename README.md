Amir Gerald G. Gilbuena Submission for Embedded Systems LAB EXERCISE 05 PREFI

Link for the video simulation:

https://youtu.be/D6F2LDdB2Do

Link for the tinkercad file:

https://www.tinkercad.com/things/kTuuqBWsug8/editel?returnTo=%2Fdashboard&sharecode=t9fnrcYGOdn51c9DmiySphlT2UgHqKbnkcXPcMOQvv4

Can't upload code since it's in tinkercad so i'll drop it here.

const int M11 = 5;
const int M12 = 6;
const int M21 = 9;
const int M22 = 10;

const int LED_FWD   = 2;
const int LED_REV   = 3;
const int LED_LEFT  = 4;
const int LED_RIGHT = 7;

void drive(int m11, int m12, int m21, int m22) {
  digitalWrite(M11, m11);
  digitalWrite(M12, m12);
  digitalWrite(M21, m21);
  digitalWrite(M22, m22);
}

void lights(int fwd, int rev, int left, int right) {
  digitalWrite(LED_FWD, fwd);
  digitalWrite(LED_REV, rev);
  digitalWrite(LED_LEFT, left);
  digitalWrite(LED_RIGHT, right);
}

void setup() {
  Serial.begin(9600);

  pinMode(M11, OUTPUT);
  pinMode(M12, OUTPUT);
  pinMode(M21, OUTPUT);
  pinMode(M22, OUTPUT);
  pinMode(LED_FWD, OUTPUT);
  pinMode(LED_REV, OUTPUT);
  pinMode(LED_LEFT, OUTPUT);
  pinMode(LED_RIGHT, OUTPUT);

  drive(0, 0, 0, 0);
  lights(0, 1, 0, 0);
  Serial.println("Ready. Send F, B, L, R or S.");
}

void loop() {
  if (Serial.available() > 0) {
    char cmd = Serial.read();

    switch (cmd) {
      case 'F': case 'f': drive(0, 0, 0, 1); lights(1, 0, 0, 0); Serial.println("Forward");  break;
      case 'B': case 'b': drive(0, 0, 1, 0); lights(0, 1, 0, 0); Serial.println("Backward"); break;
      case 'R': case 'r': drive(1, 0, 0, 1); lights(1, 0, 0, 1); Serial.println("Right");    break;
      case 'L': case 'l': drive(0, 1, 0, 1); lights(1, 0, 1, 0); Serial.println("Left");     break;
      case 'S': case 's': drive(0, 0, 0, 0); lights(0, 1, 0, 0); Serial.println("Stop");     break;
      default: break;
    }
  }
}


