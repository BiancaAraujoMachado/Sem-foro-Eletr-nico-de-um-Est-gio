# Semaforo-Eletronico-de-um-Estágio
#include "io430.h"
/* Projeto: Semáforo Eletrônico de um Estágio
Descrição: Este faz a comutação entre as cores: Verde, Amarelo e Vermelho durante
o devido tempo.*/
/*Sub-rotina: tempo
Função: Estabelece o tempo passado como parâmetro em segundos, sendo este um 
multiplicador de tempo.*/
void tempo(unsigned int x) {
  unsigned int y;
  while(x!=0) {         //Enquanto x for diferente de 0
  for(y=0;y<150;y++)    //Loop de 1ms para clock de 750kHz
    x--;                //Decrementa um em x
  }
}
/*Sub-rotina:Verde
Função: Acende o led verde durante x segundos
Entradas: -
Saídas:Bit 0 da porta 1*/
void Verde (void) {
  P1OUT|=0x01;          // Acender led verde
  tempo(25000);         //Define atraso de 25 segundos
  P1OUT&=0xFE;          //Apagar led verde
}
/*Sub-rotina:Amarelo
Função: Acende o led amarelo durante x segundos
Entradas: -
Saídas:Bit 1 da porta 1*/
void Amarelo (void) {
  P1OUT|=0x02;          // Acender led amarelo
  tempo(5000);         //Define atraso de 5 segundos
  P1OUT&=0xFD;         //Apagar led amarelo
}
/*Sub-rotina:Vermelho
Função: Acende o led vermelho durante x segundos
Entradas: -
Saídas:Bit 2 da porta 1*/
void Vermelho (void) {
  P1OUT|=0x04;          // Acender led vermelho
  tempo(20000);         //Define atraso de 20 segundos
  P1OUT&=0xFB;          //Apagar led vermelho
}
void main( void )
{
  // Stop watchdog timer to prevent time out reset
  WDTCTL = WDTPW + WDTHOLD;
  P1DIR|=0x07;          //Definir bits 0,1 e 2 da porta 1 como saída
  P1OUT=0;              //Zerar saídas da porta 1
  
  while(1) {            //Loop infinito
   Verde();             //Chama a sub-rotina verde
   Amarelo();           //Chama a sub-rotina amarelo
   Vermelho();          //Chama a sub-rotina vermelho
  }
}
