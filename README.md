<h1 align ="center"> SNMP ⚙</h1>

<img src="https://github.com/RAFAELSILVASALES/SNMP/blob/main/WhatsApp%20Image%202024-08-14%20at%2015.33.44.jpeg" width="500">

## SNMP

<br/>
O protocolo SNMP (Simple Network Management Protocol) é um protocolo amplamente utilizado para gerenciar e monitorar dispositivos de rede, como roteadores, switches, servidores, impressoras, e outros dispositivos conectados a uma rede IP. Ele permite que administradores de rede coletem informações sobre o desempenho, configurem dispositivos e diagnostiquem problemas de maneira centralizada.


<br/>
Primeiramente, vamos instalar o protocolo SNMP em uma distribuição Linux. Neste exemplo, estou usando o Kali, mas os comandos são bastante semelhantes aos do Ubuntu, por exemplo.


```
$ sudo apt update
```
```
$ sudo apt install snmp snmpd
```

 Após a instalação, você pode iniciar e verificar o status do serviço SNMPD (demon SNMP) com os seguintes comandos:

Para iniciar o serviço SNMPD:
```
$ sudo systemctl status snmpd
```

Para verificar o status do serviço:
```
$ sudo systemctl status snmpd
```

Configuração (opcional): Para configurar o SNMP de acordo com as suas necessidades, você pode editar o arquivo de configuração localizado em /etc/snmp/snmpd.conf.

Lembre-se de que algumas configurações podem exigir que você reinicie o serviço para que as alterações tenham efeito:
```
$  sudo systemctl restart snmpd
```
Agora vamos acessar o arquivo de configuração que está localizado em /etc/snmp/snmpd.conf.

<img src="https://github.com/RAFAELSILVASALES/SNMP/blob/main/5028516752488770994.jpg" width="500">
```
Esta imagem ilustra como configurar o SNMP. Precisamos criar duas comunidades: uma destinada à leitura das informações e outra para permitir a escrita. Os nomes dessas comunidades podem ser definidos conforme sua preferência.



 Configurar a Comunidade SNMP
A "comunidade SNMP" é um nome de grupo que age como uma senha, permitindo que o dispositivo seja consultado ou configurado remotamente.

Leitura-Escrita (rw): Permite tanto a consulta quanto a configuração do dispositivo.
Somente Leitura (ro): Permite apenas a consulta.

 Configurar o switch 

Exemplo de configuração para comunidade somente leitura (ro):
```
$ Switch(config)# snmp-server community profitecRO ro

```
Exemplo de configuração para comunidade leitura-escrita (rw):
```
$ Switch(config)# snmp-server community profitecRW rw
```
 Configurar Host de Destino para Traps SNMP
Os "Traps SNMP" são mensagens enviadas pelo switch para informar um sistema de gerenciamento de rede (NMS) sobre eventos importantes.


```
$ Switch(config)# snmp-server host 192.168.1.100 version 2c profitecRW

```

```
$ Switch(config)# snmp-server host 192.168.1.100 version 2c profitecRO

```


A MIB (Management Information Base) é um conjunto de objetos gerenciáveis em uma rede. Cada objeto na MIB é identificado por um OID (Object Identifier), que pode ser usado para monitorar e gerenciar dispositivos de rede como switches Cisco.

Aqui estão alguns OIDs comuns da MIB que você pode usar para monitorar um switch Cisco:

1. SysName (Nome do Sistema)
OID: .1.3.6.1.2.1.1.5
Descrição: Retorna o nome do dispositivo (hostname).
2. SysUpTime (Tempo de Atividade do Sistema)
OID: .1.3.6.1.2.1.1.3
Descrição: Retorna o tempo desde a última reinicialização do dispositivo.
3. SysLocation (Localização do Sistema)
OID: .1.3.6.1.2.1.1.6
Descrição: Retorna a localização física do dispositivo.
4. SysContact (Contato do Sistema)
OID: .1.3.6.1.2.1.1.4
Descrição: Retorna o contato responsável pelo dispositivo.
5. ifDescr (Descrição da Interface)
OID: .1.3.6.1.2.1.2.2.1.2
Descrição: Retorna a descrição da interface de rede.
6. ifInOctets (Bytes Recebidos na Interface)
OID: .1.3.6.1.2.1.2.2.1.10
Descrição: Retorna o número de bytes recebidos em uma interface de rede.
7. ifOutOctets (Bytes Enviados na Interface)
OID: .1.3.6.1.2.1.2.2.1.16
Descrição: Retorna o número de bytes enviados a partir de uma interface de rede.
8. ifOperStatus (Status Operacional da Interface)
OID: .1.3.6.1.2.1.2.2.1.8
Descrição: Retorna o status operacional da interface (up, down, testing).
9. ifAdminStatus (Status Administrativo da Interface)
OID: .1.3.6.1.2.1.2.2.1.7
Descrição: Retorna o status administrativo da interface (up, down, testing).
10. dot1dTpFdbAddress (Endereço MAC da Tabela de Bridge)
OID: .1.3.6.1.2.1.17.4.3.1.1
Descrição: Retorna os endereços MAC conhecidos pela tabela de bridge do switch.
11. dot1dTpFdbPort (Porta da Tabela de Bridge)
OID: .1.3.6.1.2.1.17.4.3.1.2
Descrição: Retorna a porta correspondente ao endereço MAC na tabela de bridge.
12. CISCO-CDP-MIB (Informações CDP - Cisco Discovery Protocol)
OID: .1.3.6.1.4.1.9.9.23
Descrição: Permite monitorar dispositivos Cisco vizinhos através do CDP.
13. CISCO-STACK-MIB (Informações de Stack)
OID: .1.3.6.1.4.1.9.5.1.1
Descrição: Retorna informações sobre a pilha de dispositivos Cisco, incluindo status e número de unidades na pilha.
14. CISCO-MEMORY-POOL-MIB (Monitoramento de Memória)
OID: .1.3.6.1.4.1.9.9.48
Descrição: Permite monitorar a utilização da memória em dispositivos Cisco.
15. CISCO-CPU-MIB (Monitoramento de CPU)
OID: .1.3.6.1.4.1.9.2.1.57
Descrição: Permite monitorar a utilização da CPU em dispositivos Cisco.
Como Usar esses OIDs
Esses OIDs podem ser usados com comandos SNMP como snmpget, snmpwalk, ou ferramentas de monitoramento de rede como Nagios, Zabbix, ou Cacti

 Exemplo de uma MIB

<img src="https://github.com/RAFAELSILVASALES/SNMP/blob/main/5028516752488770993.jpg" width="500">
# Capturar de trafego do SNMP 
<img src="https://github.com/RAFAELSILVASALES/SNMP/blob/main/5028774381807053853.jpg" width="500">

