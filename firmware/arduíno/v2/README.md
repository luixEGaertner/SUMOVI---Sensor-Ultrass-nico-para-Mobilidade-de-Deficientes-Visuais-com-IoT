// --- Definições de Pinos para Três Sensores ---
// Sensor 1
const int TRIG_PIN_S1 = 9;
const int ECHO_PIN_S1 = 10;

// Sensor 2
const int TRIG_PIN_S2 = 6;
const int ECHO_PIN_S2 = 7;

// Sensor 3
const int TRIG_PIN_S3 = 4;
const int ECHO_PIN_S3 = 5;

// Pinos de Saída
const int ledPin = 12;
const int buzzerPin = 2;     // Agora buzzer no pino 2
const int vibPin = 3;        // Motor vibratório no pino 3 (PWM)

// Parâmetros de Medição e Alerta
const unsigned long timeout_us = 30000UL; // 30 ms (5 m)
const float tblind_us = 100.0;            // Tempo cego
const float dmin_cm = 2.0;                
const float alert_max_cm = 200.0;

// Estrutura dos sensores
struct Sensor {
  int trigPin;
  int echoPin;
  float distance;
};

Sensor sensors[] = {
  {TRIG_PIN_S1, ECHO_PIN_S1, 0.0},
  {TRIG_PIN_S2, ECHO_PIN_S2, 0.0},
  {TRIG_PIN_S3, ECHO_PIN_S3, 0.0}
};

const int NUM_SENSORS = sizeof(sensors) / sizeof(sensors[0]);

// --- Setup ---
void setup() {
  Serial.begin(9600);

  for (int i = 0; i < NUM_SENSORS; i++) {
    pinMode(sensors[i].trigPin, OUTPUT);
    pinMode(sensors[i].echoPin, INPUT);
    digitalWrite(sensors[i].trigPin, LOW);
  }

  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(vibPin, OUTPUT);

  Serial.println("Sistema inicializado.");
}

// Função de medição individual
float measureDistance(int trigPin, int echoPin) {

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  unsigned long duration = pulseIn(echoPin, HIGH, timeout_us);

  if (duration == 0) {
    return alert_max_cm + 1.0;
  }

  float distance_cm = duration / 58.0;
  float dBlind_cm = tblind_us / 58.0;
  float dreal_cm = distance_cm - dBlind_cm;

  if (dreal_cm < dmin_cm) dreal_cm = dmin_cm;

  return dreal_cm;
}

void loop() {
  bool alertTriggered = false;

  Serial.println("---");

  // Medição sequencial
  for (int i = 0; i < NUM_SENSORS; i++) {
    float dreal_cm = measureDistance(sensors[i].trigPin, sensors[i].echoPin);
    sensors[i].distance = dreal_cm;

    Serial.print("S"); Serial.print(i + 1);
    Serial.print(" d(cm): "); Serial.println(dreal_cm, 2);

    if (dreal_cm <= alert_max_cm) {
      alertTriggered = true;
    }

    delay(50);
  }

  // Verificar menor distância
  float min_distance = alert_max_cm + 1.0;
  for (int i = 0; i < NUM_SENSORS; i++) {
    if (sensors[i].distance < min_distance) {
      min_distance = sensors[i].distance;
    }
  }

  // LÓGICA DE ALERTA
  if (alertTriggered) {

    digitalWrite(ledPin, HIGH);

    // Se for buzzer ativo:
    digitalWrite(buzzerPin, HIGH);

    // Intensidade do motor proporcional
    int pwmValue = 0;

    if (min_distance <= 5) pwmValue = 255;
    else if (min_distance <= 20) pwmValue = 200;
    else if (min_distance <= 50) pwmValue = 150;
    else if (min_distance <= 100) pwmValue = 100;
    else if (min_distance <= 150) pwmValue = 60;
    else pwmValue = 30;

    analogWrite(vibPin, pwmValue);

  } else {

    digitalWrite(ledPin, LOW);
    digitalWrite(buzzerPin, LOW);
    analogWrite(vibPin, 0);

  }

  delay(120);
}
