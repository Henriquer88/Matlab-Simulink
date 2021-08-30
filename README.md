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

 Para fazermos a comunicção do Simulink com qualquer hardware devemo instalar o toolbox **Instrument Control 
 
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
 



