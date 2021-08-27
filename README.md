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
Vamos utilizar a placa F401 para ler os pulso de um encolder e enviar os dados pela serial 





