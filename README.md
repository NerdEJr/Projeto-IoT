# Projeto de IoT - Codificação Morse com Arduino
Descrição:
Este projeto foi desenvolvido como parte da disciplina de Microcontroladores e IoT, com o objetivo principal de utilizar um Arduino para codificar mensagens digitadas pelo usuário em código Morse. A implementação inclui a utilização de um LED para a saída visual da mensagem codificada e uma exibição da mensagem na tela.

## Funcionalidades Principais:
**Entrada de Mensagem:** Permite que o usuário digite uma mensagem por meio de uma interface simples.
Codificação em Código Morse: Utilizando a lógica de codificação Morse, a mensagem digitada é transformada em sequências de luz (LED) representando os caracteres Morse correspondentes.

**Saída Visual com LED:** Um LED é utilizado para exibir a mensagem codificada visualmente, proporcionando uma experiência interativa.
Feedback na Tela: Além da saída visual, a mensagem codificada é exibida na tela, tornando o projeto acessível e intuitivo.

**Objetivo:**
Explorar os conceitos práticos de Microcontroladores e IoT, integrando a codificação Morse para comunicação. Este projeto visa aprimorar a compreensão da programação de Arduino, entrada e saída de dados, e a aplicação prática de conceitos de IoT em um contexto educacional.

## Tecnologias Utilizadas:
Arduino (ou especificar o modelo utilizado)
Linguagem de Programação C++
Conceitos de IoT e Microcontroladores

## Projeto Digital (Thinkercad)

![alt text](https://github.com/NerdEJr/Projeto-IoT/blob/main/Imagens/PROJETO%20IoT.png?raw=true)

**Como Executar:**
Clone este repositório.
Carregue o código no seu Arduino utilizando a IDE.
Digite sua mensagem na interface indicada.
Observe a saída visual no LED e a mensagem na tela.

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
## Imagens

![alt text](https://github.com/NerdEJr/Projeto-IoT/blob/main/Imagens/image2.jpeg?raw=true)
![alt text](https://github.com/NerdEJr/Projeto-IoT/blob/main/Imagens/image3.jpeg?raw=true)
![alt text](https://github.com/NerdEJr/Projeto-IoT/blob/main/Imagens/image1.jpeg?raw=true)

## Vídeo de Apresentação
https://www.youtube.com/watch?v=6Yfij6RwoLE
