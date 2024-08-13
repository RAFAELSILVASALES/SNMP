<h1 align ="center"> SNMP ⚙</h1>

<img src="https://github.com/RAFAELSILVASALES/SNMP/blob/main/5028774381807053853.jpg" width="320">

## SNMP

<br/>
Netmiko é uma biblioteca Python que facilita a conexão e interação com dispositivos de rede, como roteadores e switches. Ele se baseia na biblioteca Paramiko para realizar conexões SSH.

Basicamente, o Netmiko facilitar a configuração de vários dispositivos, permitindo que você envie comandos, leia saídas e faça alterações de configuração.

A biblioteca fornece suporte a vários fabricantes e modelos de dispositivos de rede, como Cisco IOS, Juniper, HP e outros. Ele fornece classes e métodos específicos para cada tipo de dispositivo, facilitando a interação.

<br/>
Primeiramente, vamos instalar o protocolo SNMP em uma distribuição Linux. Neste exemplo, estou usando o Kali, mas os comandos são bastante semelhantes aos do Ubuntu, por exemplo.
## Instalar

```
$ sudo apt update
$ sudo apt install snmp snmpd

## Após a instalação, você pode iniciar e verificar o status do serviço SNMPD (demon SNMP) com os seguintes comandos:

Para iniciar o serviço SNMPD:
$ sudo systemctl status snmpd
Para verificar o status do serviço:
$ sudo systemctl status snmpd

Configuração (opcional): Para configurar o SNMP de acordo com as suas necessidades, você pode editar o arquivo de configuração localizado em /etc/snmp/snmpd.conf.

Lembre-se de que algumas configurações podem exigir que você reinicie o serviço para que as alterações tenham efeito:
$  sudo systemctl restart snmpd

```

- <a href="https://pypi.org/project/netmiko/"> Documentação </a>

## Também a opção de criar um ambiente virtual

Para Windows:
Digite no Terminal

```
$ python -m venv   venv
```

A ativar o ambiente virtual

```
$ /venv/Scripts/Activate.ps1
```

Instalar a biblioteca:

```
$ pip install netmiko

```

Para Linux:
Digite no Terminal

```
$ pip3 install virtualenv
```

Para verificar a instalação, digite:

```
$ virtualenv --version
```

Para criar um ambiente virtual python digite no terminal:

```
$ virtualenv <venv>
```

Para ativar o ambiente, digite:

```
$ cd venv
$ source bin/activate

```

Instalar a biblioteca:

```
$ pip3 install netmiko

```

## Exemplo ----

```py
from netmiko import ConnectHandler

- Dicionário para definir os parâmetros do dispositivo
  device = {
  'device_type': 'cisco_xe',
  'ip': '192.168.32.68',
  'username': 'admin',
  'password': 'cisco'
  }
# Conexão via SSH
  connect = ConnectHandler(**device)

# ConnectHandler(): Esse é o método que inicia uma conexão com o dispositivo.

print(connect.find_prompt())

output = connect.send_command("show ip arp")

# send_command(): É o método para enviar um comando para o dispositivo.

config_commands = [
"enable",
"configure t",
"line console 0",
"password cisco",
"login",
"exit",
"enable secret cisco",
"banner motd # ACESSO PROIBIDO # ",
"line vty 0 4",
"password cisco",
"login ",
"exit",
"service password-encryption",
"security passwords min-length 5",
"login block-for 120 attempts 3 within 30",
]

cfg_output = connect.send_config_set(config_commands)

# send_config_set(): Este é um método pode ser usado para enviar uma lista de comandos de configuração para o dispositivo.

print(cfg_output)
```

## Exemplo:

- [Exemplo Netmiko](readme_ex.md)
- [Backup](https://github.com/RAFAELSILVASALES/network_automation/blob/main/readme_ex_backup.md)

## Em breve mais conteúdo sobre automação de redes.

##
