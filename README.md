# Projeto-IoT

## Imagens

Imagens/390ed66e-d78e-49ee-ab28-f87c3276abdb.jfif
Imagens/62a7c4fc-b50d-45b8-9a8d-db55bf4a316d.jfif
Imagens/8cef634c-4656-49b3-8d1a-69baa1472140.jfif

## Código-Fonte
```C#
int LED = 2;
char alfabeto[37] = {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h',
                     'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q',
                     'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
                     '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', ' '
                    };
char morse[37][7] = {{ "o- "}, {"-ooo "}, {"-o-o "}, {"-oo "}, {"o "}, {"oo-o "},
  {"--o "}, { "oooo "}, {"oo " }, {"o--- "}, {"-o- "}, {"o-oo "},
  {"-- "}, {"-o "}, {"--- "}, { "o--o "}, {"--o- "}, { "o-o "},
  {"ooo "}, {"- "}, {"oo- "}, {"ooo- "}, {"o-- "}, {"-oo- "},
  {"-o-- "}, {"--oo "}, {"o---- "}, {"--oo- "}, {"ooo-- "},
  {"oooo- "}, {"ooooo "}, {"-oooo "}, {"--ooo "}, {"---oo "},
  {"----o "}, {"----- "}, {" "}
};

String nome;

char ligaLed[2] = {'o', '-'};
int esperaCurto = 200, esperaLongo = 600, esperaEntre = 1000;


void setup() {
  Serial.begin(9600);
  pinMode(LED, OUTPUT);
}

void loop() {
  Serial.println("Digite a frase que deseja codificar:");
  // apenas responde quando dados são recebidos:
  while (Serial.available() == 0) {}
  // lê do buffer o dado recebido:
  nome = Serial.readString();
  nome.toLowerCase();
  Serial.println("Frase em Morse:");
  // responde com o codigo codificado:
  for (int i = 0; nome[i] != 0; i++) {
    for (int j = 0; alfabeto[j] != 0; j++) {
      if (nome[i] == alfabeto[j]) {
        Serial.print(morse[j]);
        for (int k = 0; morse[j][k] != 0; k++) {
          if (morse[j][k] == ligaLed[0]) {
            digitalWrite(LED, HIGH);
            delay(esperaCurto);
            digitalWrite(LED, LOW);
            delay(esperaCurto);
          }
          if (morse[j][k] == ligaLed[1]) {
            digitalWrite(LED, HIGH);
            delay(esperaLongo);
            digitalWrite(LED, LOW);
            delay(esperaCurto);
          }
        }
        delay(esperaEntre);
      }
    }
  }
  Serial.println();
  Serial.println();
}
```
