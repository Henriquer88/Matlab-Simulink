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

* Dados enviados para serial 

<a href="https://imgur.com/gps1j1M"><img src="https://i.imgur.com/gps1j1M.png" title="source: imgur.com" /></a>

 Esse programa faz a contagem dos pulsos de um encoder acoplado a um motor 
 
 # Criando uma interface no Simulink-Matlab
 
* No **Command Window** do Matalab basta digitar o comando **simulink** para abrir o software 
 
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

* Com o query já inserido no projeto, vamos agora fazer as configurações necessárias  

<a href="https://imgur.com/HiIuWom"><img src="https://i.imgur.com/HiIuWom.png" title="source: imgur.com" /></a>

* Clicando sobre o bloco query teremos acesso as configurações 

 Nessa tela  podemos configurar tipo de interface, baudrate, buffer etc.
 
<a href="https://imgur.com/bYz8JX0"><img src="https://i.imgur.com/bYz8JX0.png" title="source: imgur.com" /></a>

 * Agora vamos configurar qual o formato dos dados**ASC II format string** e quantos Frames **Frame size** vamos enviar ao Simulink

<a href="https://imgur.com/mFqQ571"><img src="https://i.imgur.com/mFqQ571.png" title="source: imgur.com" /></a>

  Nesse exemplo iremos enviar dados no formato int e apenas um frame
  
  
  
  #  Utilizando um Dashboard
 
 *  Configurado o bloco Query agora precisamos exibir os dados vindo da serial do microcontrolador, o bloco utilizado é um **Display**

  <a href="https://imgur.com/3TbdNTd"><img src="https://i.imgur.com/3TbdNTd.png" title="source: imgur.com" /></a>
  
  * Para esse exemplo vamos configurar nosso display para o formato Short
   
   <a href="https://imgur.com/nch1MCq"><img src="https://i.imgur.com/nch1MCq.png" title="source: imgur.com" /></a>
  
  * Em **Library Browser** podemos encontrar alguns Dashboard para usar em nossa interface

  <a href="https://imgur.com/vDmaAD4"><img src="https://i.imgur.com/vDmaAD4.png" title="source: imgur.com" /></a>
  
  Para essa aplicação vamos usar o **Custon Gauge**
  
<a href="https://imgur.com/R0ymv8E"><img src="https://i.imgur.com/R0ymv8E.png" title="source: imgur.com" /></a>

  Com esse modelo podemos configurar os ponteriros, colocar limites e mudadr as cores

## Configuração do Gauge

 Com o **Gauge** inserido em nosso projeto, vamos mexer nas configurações
 
 <a href="https://imgur.com/Lkb9prS"><img src="https://i.imgur.com/Lkb9prS.png" title="source: imgur.com" /></a>
 
  * Clicando duas vezes sobre o **Gauge** será aberto uma janela com os parâmetros bloco **Block Parametrs Custom Gauge**

<a href="https://imgur.com/syd5PFX"><img src="https://i.imgur.com/syd5PFX.png" title="source: imgur.com" /></a>

* Primeira coisa  que vamos fazer será selecionar o sinal que vamos monitorar, clicando com o botão do mouse sobre a conecxão entro o bloco **Query** e o **Display** feito isso agora basta clicar em **CONNECT**  

<a href="https://imgur.com/nroda6O"><img src="https://i.imgur.com/nroda6O.png" title="source: imgur.com" /></a>

* Nessa janela podemos limitar o valor do ponteiro do **Gauge** e adicionar uma escala de cores.

<a href="https://imgur.com/knaajKu"><img src="https://i.imgur.com/knaajKu.png" title="source: imgur.com" /></a>

* Podemos também adicionar uma área onde iremos plotar os dados do microcontrolador, para esse exemplo foi usado o bloco **Dashboard Scope**

<a href="https://imgur.com/svgcevm"><img src="https://i.imgur.com/svgcevm.png" title="source: imgur.com" /></a>

Assim como o bloco **Gauge** temos que fazer a configuração  **DashBoard Scope**

<a href="https://imgur.com/PwSZHVS"><img src="https://i.imgur.com/PwSZHVS.png" title="source: imgur.com" /></a>

* Antes de fazer rodar a simulação devemos ir em **Stop Time** e digitar **inf** , pois queremos fazer a aquisição dos dados em tempo real  

<a href="https://imgur.com/q7MjbdF"><img src="https://i.imgur.com/q7MjbdF.png" title="source: imgur.com" /></a>

Pronto, agora vamos  capturar os dados do microcontrolador.














 
 











  
  
 
 

