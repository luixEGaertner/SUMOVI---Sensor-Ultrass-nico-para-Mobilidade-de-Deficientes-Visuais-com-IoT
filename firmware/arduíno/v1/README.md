// ===============================
// DEFINIÇÃO DOS PINOS
// ===============================
// >>> TROQUE AQUI PARA TESTAR CADA SENSOR <<<
//
// Exemplo:
// Sensor 1 -> TRIG = 2 / ECHO = 3
// Sensor 2 -> TRIG = 4 / ECHO = 5
// Sensor 3 -> TRIG = 6 / ECHO = 7
//
#define TRIG_PIN 2   // <-- MUDE ESTE PINO
#define ECHO_PIN 3   // <-- MUDE ESTE PINO

// ===============================

long duracao;
float distancia;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);

  Serial.begin(9600);
  Serial.println("Teste individual do sensor ultrassonico");
}

void loop() {
  // Garante TRIG em nível baixo
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  // Pulso de 10 µs no TRIG
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Mede o tempo do eco (em microssegundos)
  duracao = pulseIn(ECHO_PIN, HIGH, 30000);
  // timeout de 30 ms (~5 m)

  if (duracao == 0) {
    Serial.println("Sem eco detectado");
  } else {
    // Cálculo da distância
    distancia = (duracao * 0.0343) / 2;

    Serial.print("Distancia: ");
    Serial.print(distancia);
    Serial.println(" cm");
  }

  delay(500); // intervalo entre leituras
}
