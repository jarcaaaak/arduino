#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

int buzzerPin = 9;

float fireTemp = 27.0;

void setup() {
  Serial.begin(9600);
  dht.begin();
  pinMode(buzzerPin, OUTPUT);
}

void loop() {

  float temp = dht.readTemperature();

  if (isnan(temp)) {
    Serial.println("ERROR");
    return;
  }

  if (temp >= fireTemp) {
    tone(buzzerPin, 1000);
    Serial.println("FIRE");
    noTone(buzzerPin);
    Serial.println("SAFE");
  }

  delay(1000);
}
