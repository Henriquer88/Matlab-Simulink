# Matlab-Simulink
# Objetivo
Tutorial de como criar uma interface gráfica no ambiente Matlab/Simulink

# Softwares e Hardwares  necessários 
* Matlab - Versão 2017 
* Nucleo Stm32 F401
* Mbed 

# Introdução 
Nesse tutorial iremos mostrar como fazer a comunicação entre hardware e Simulink. Para esse exemplo vamos  utilizar a placa F401 para enviar pela serial os dados de um encoder. 

# Instalação de Toolbox

 Para fazermos a comunicção do Simulink com qualquer hardware devemo instalar o toolbox **Instrument Control** 
 
<a href="https://imgur.com/8vvmKyQ"> <img src="https://i.imgur.com/8vvmKyQ.png" title="source: imgur.com" /></a>

Com o **Instrument Control Toolbox, você pode gerar dados no MATLAB para enviar a um instrumento ou ler dados no MATLAB para análise e visualização. Você pode automatizar testes, verificar projetos de hardware. O Toolbox fornece suporte integrado para protocolos seriais TCP / IP, UDP, I2C, SPI e Bluetooth.

# Enviando dados pela serial 
* Nesse exemplo iremos utilizar um códido em MBED para enviar dados da leitura de um encoder

```javascript
#include "mbed.h"

InterruptIn Signal_A(D7);

Serial pc(USBTX, USBRX,115200);

int main()
{

    Signal_A.rise(&signal);

    while(1) {

        wait_ms(400);
        rpm = rpm/500;
        pc.printf(" %1.0i \n\r",rpm);
        rpm= 0;
    }
}

```
 Esse programa faz a contagem dos pulsos de um encolder, os dados lidos pelo microcontrolador serão enviados para o Matlab/Simulink
 
 # Criando uma interface no Simulink-Matlab
 
* No **Command Window** do Matalab basata digitar o comando **simulink** para abrir o software 
 
 <a href="https://imgur.com/FHxaozi"><img src="https://i.imgur.com/FHxaozi.png" title="source: imgur.com" /></a>
 
 * Em **Simulink Start Page** vamos crair um **Blank Model** 
  
 <a href="https://imgur.com/NCocRDd"><img src="https://i.imgur.com/NCocRDd.png" title="source: imgur.com" /></a>
 
 * Com  um modelo em branco criado vamos agora inserir blocos para criação de interface gráfica
 
 <a href="https://imgur.com/FmQXPz4"><img src="https://i.imgur.com/FmQXPz4.png" title="source: imgur.com" /></a>
 
 # Criando a estrutura para a interface gráfica 
 
 Primerio bloco que iremos incluir em nosso projeto é o **Query Instrument** ele de forma resumida é o responsável por fazer a conexção entre o Simulink e o microcontrolador 
 
* Em  **Library Browser** temos acaesso  a todos os blocos de ferramentas que o Similunk disponibiliza 
 
 <a href="https://imgur.com/UqNxRIB"><img src="https://i.imgur.com/UqNxRIB.png" title="source: imgur.com" /></a>
 
* Clicando sobre o icone **Libray** é aberto a janela **Simulink Library Browser** 
 
 <a href="https://imgur.com/s9JSBqC"><img src="https://i.imgur.com/s9JSBqC.png" title="source: imgur.com" /></a>
 
* Nela vamos buscar pelo bloco **Query Instrument**
 
 <a href="https://imgur.com/EebjXwN"><img src="https://i.imgur.com/EebjXwN.png" title="source: imgur.com" /></a>
 
 * Clicando com o botão direito sobre o bloco selecionamos **add block**
 
 <a href="https://imgur.com/woi8zjh"><img src="https://i.imgur.com/woi8zjh.png" title="source: imgur.com" /></a>
 
 
 ## Configurando o bloco Query

Com o query já inserido no projeto, vamos agora dar duplo click sobro o bloco 


 
 

