# -#include <SoftwareSerial.h>
SoftwareSerial Bt(10, 11); //10Pin-TX(HC06),11Pin-RX(HC06)
void setup() {
  Bt.begin(9600);
  Serial.begin(9600);
}
void loop() {
  while (1) {
    int a = analogRead(A0);
    Serial.println(a);
    delay(500);
    if (a > 150) { //조도가 150이상일시 
      Bt.print("wake up"); //스마트폰에"wake up"을 전송함
      delay(1000);
    }
    if (Bt.available()) {
      String m = Bt.readString();
      if (m.indexOf("stop") == 0) exit(0);// 스마트폰에서 stop이 오면 종료
     }
  }
}

