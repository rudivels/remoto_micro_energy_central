# Central de monitoramento e acionamento a distância de micro usinas de geração de energia elétrica em comunidades remotas

Rudivels @ março 2020

`/Users/rudi/Documentos/GitHub/Central_remota_usina`

# 1. Apresentação
Este projeto surgiu da necessidade de acompanhar o funcionamento das diversas instalações de geração descentralizada de energia elétrica espalhadas em comunidades remotas no Brasil. 

A primeira instalação que tive a oportunidade de ajudar a instalar foi uma turbina hidrocinética, ainda na década de 1990, e desde então, acompanhei diversas instalações com turbinas Pelton, turbinas Indalma, paineis fotovoltaicos, motores a combustão com gaseificação de biomassa e a combinação dessas tecnologias. 

Muitas dessas tecnologias foram desenvolvidas ou implementados pelo Laboratório de Energia e Ambienta da Faculdade de Tecnologia da UnB e a partir de 2008 pelo curso de Engenharia de Energia da Faculdade de Engenharia da UnB campus Gama.

Um dos desafios nestes sistemas sempre foi o monitoramento do seu funcionamento com equipamentos de custo acessíveis implementados com  tecnologias (hardware e software) abertas e disponiveis no mercado nacional. 

As grandes distâncias dessas instalações ao centro urbano mais próximo e a dificuldade de acesso trazem uma complicação adicional e demandam que o sistema de monitoramento devam ser bastante robusto e confiável. Além disso há o desafio da telecomunicação com o sistema remota, que depende das tecnologias de rádio, telefonia e internet disponíveis nas localidades.

Neste texto, vamos apresentar as tecnologias que implementamos nos últimos vinte anos em diversos sítios e a partir dessas experiências propor uma arquitetura de monitoramento e acionamento remoto. 

O texto pretende ser bastante didático e detalhado para que o sistema possa ser implementado por qualquer estudante/profissional com conhecimento básico de eletrônica, programação e redes de computadores.

Vamos iniciar com um exemplo de central de monitoramento usando um Sistema Supervisório (ScadaBR) no sítio da usina (onsite) e depois introduzir o desafio de fazer o monitoramento remoto. 

# 2. Introdução      

Geração descentralizada de energia elétrica é uma das opções para atender comunidades distantes das redes de distribuição com serviços de eletricidade. 
Há diversas tecnologias e fontes de energia que podem ser usados para este fim. Há também diversas escalas que estes sistemas poder ter. Convencionamos neste trabalho: 

- pico usina com capacidade instalada até 1kW; 
- micro usina com capacidade instalada ate 10 kW;
- mini usina com capacidade instalada até 100kW;

As tecnologias de conversão e suas fontes de energia:

- Motor de combustão interno com diesel
- Motor de combustão interno com biomassa
- Hidrelétrica, incluindo hidrocinética
- Painel Solar Fotovoltaico
- Turbina Eólica
- Sistemas Híbridos

Desafios tecnologicas
 
- Manutenção corretiva e preditiva
- Monitoramento da operação 
- Capacitação de operadores locais


Nessa secção serão apresentados alguns exemplos de pico usinas. Se trata de um trabalho em andamento e a documentação será atualizada na medida que os sistemas são implementados. 

## 2.1. Pico usina com turbina Pelton -  Imperial 
Este Pico Usina de Geração de Energia elétrica foi implementado num sítio em Brazlândia-DF em 2008 por estudantes da empresa junior de energia elétrica da UnB e tem uma capacidade instalada de 2 kW e atende um empreendimento de eco turismo.

O sítio é alimentado únicamento com essa usina e atende, restaurante, escritório, alguns chalés e um residência do caseiro.

Este artigo apresenta o trabalho realizado pelos estudantes do curso de engenharia de energia em 2012 [link para artigo](https://fga.unb.br/rudi.van/galeria/artigos-diversos/analise-de-uma-usina-hidreletrica-em-um-sistema-isolado-no-distrito-federal-william-macedo-pereira-bruno-batista-suehara-e-auto.pdf)


Foto da casa de maquinas
![](fotos/casa_maquinas_mico_central_imperial.jpg)

Detalhe da casa de máquina com Roda Pelton
![](fotos/turbina_micro_central_imperial.jpg)

Ficha técnica

| Especificação  | valor | unidade | 
|----------------|:-----:|:-------:|
| Potência       |  2    | kW      |     
| Vazão          |  xx   | lit/seg |     
| Máquina hidraulica  | Roda Pelton |     
| Quantidade turbinas | 1 | unidades |  
| Gerador trifásico | 10 | KVA|  


## 2.2. Pico usina com turbina hidrocinética

A experiência com a turbina hidrocinética data de 1995 e foi instalada no Sítio Veredão no Municipio de Correntina - BA. 
Este artigo de 2003 apresenta a tecnologia e sua instalação. 
[link para artigo](https://fga.unb.br/articles/0002/5925/Els_et_al._-_2003_-_Hydrokinetic_turbine_for_isolated_villages.pdf)


## 2.3. Micro usina Açaizal do Prata

Microcentral comunitário de 80 kW que fornece energia elétrica para a comunidade de Açaizal de Prata no município de Belterra região de Santarém estado do Pará. 

[link para artigo](https://sbpe.org.br/index.php/rbe/article/view/251)

Casa de máquina da usina
![](fotos/foto_acaizal_casa_maquina.jpg)

Detalha da turbina na casa de máquina

![](fotos/foto_acaizal_turbina.jpg)

Ficha técnica

| Especificação  | valor | unidade | 
|----------------|:-----:|:-------:|
| Potência       |  80   | kW      |   
| Vazão          |  xx   | lit/seg |  
| Tipo turbina   | Indalma |   |  
| Quantidade turbinas | 2 | unidades |  
| Gerador | | |  

## 2.4. Micro usina Cachoeria do Aruã

Microcentral comunitário de 80 kW que fornece energia elétrica para a comunidade de Cachoeira Aruã no município de Santareém no estado do Pará.

Detalhe da turbina na casa de maquina de Cachoeira Aruã - 
![](fotos/foto_arua_turbina.jpg)

Ficha técnica

| Especificação  | valor | unidade | 
|----------------|:-----:|:-------:|
| Potência       |  80    | kW      |   
| Vazão          |  xx   | lit/seg |  
| Tipo turbina   | Indalma |   |  
| Quantidade turbinas | 2 | unidades |
| Gerador | | |  

# 3. Configuração geral do sistema

A operação no dia-a-dia dessas instalações deve realizado por técnicos e operadores locais. Entretanto, há a necessidade de acompanhamento do funcionamento por técnicos especialiados. Assim por meio de ligar os centrais de monitoramento nas localidades a um sistema supervisório. Acompanhamento de técnicos especilizados, podendo fazer o planejamento das manutenção preditivos baseado nos dados operacionais das instalações.  

Diagrama geral do sistema. 
![](diagrama_usina_scada.jpg)

O sistema supervisório e controle tem o nome completo de Supervisory Control and Data Aquisition (Scada) e neste trabalho será implementado pelo software [ScadaBR](https://www.scadabr.com.br/).

O ScadaBR foi desenvolvido iniciou em 2006, por iniciativa da MCA Sistemas (atualmente Sensorweb), empresa de Florianópolis que naquele ano convidou outras empresas da região (a Unis Sistemas e a Conetec), em conjunto com a Fundação CERTI e a Universidade Federal de Santa Catarina, para desenvolver um sistema SCADA completo, gratuito, em Português, especialmente desenhado para micro e pequenas empresas.

Este software Scada ja foi usado em diversos projetos na UnB em aplicações que vão desde gerenciamento de laboratórios, ensaios de equipamentos, monitoramento de equipamentos e automação predial.

Alguns trabalhos que usaram ScadaBR na UnB: 

[Bancada de ensaio](https://fga.unb.br/articles/0001/9546/TCC2_Rodrigo_de_Oliveira_Calixto_090013476.pdf)

[Controle de inversor](https://fga.unb.br/articles/0001/9545/Maria_Eugenia_TCC2.pdf)

[Controle de turbina Indalma](https://repositorio.unb.br/handle/10482/31871)

[Plataforma de instrumentação](https://repositorio.unb.br/handle/10482/24457)

[Automação predial](https://repositorio.unb.br/handle/10482/22432)

[Automação de dinamômetro](https://repositorio.unb.br/handle/10482/20432)

[Controle veiculo elétrico](https://fga.unb.br/articles/0002/5927/TCC_2_Leticia_Marinho_de_Souza_final_nov_2022.pdf)

Este trabalho focará inicialmente na micro usina e seu monitoramento da operação com o sistema supervisório instalo na usina e na medida que a pesquisa avança os demais itens serão adicionados.

Na primeira configuração o ScadaBR será instalada diretamente na usina sem a necessidade de comunicação de internet, e desse modo sem o central de monitoramento de acionamento remoto que será apresentado na secção 4.


## 3.1. ScadaBR  na usina

Principais funcionalidades:

* Monitorar a pressão na entrada da turbina
* Monitorar a vazão na entrada (saída) da turbna
* Monitorar dados de rotação da turbina (RPM)
* Monitorar temperatura da turbina e gerador
* Monitorar tensão, corrente e potência gerada
* Monitorar a frequencia da rede
* Monitorar o fator de potência da carga (rede) 


O ScadaBR tem suporte para diversos protocolos de comunicacão. Um dois mais conhecidos é o protocolo Modbus IP/RTU. 

No nosso caso específico a proposta é implementar a comunicação entre o ScadaBR e os instrumentos/medidores usando o protocolo Modbus-RTU.

Principais medidores:

* Multimedidor com protocolo Modbus-RTU
* Medidor de frequencia e temperatura com Modbus-RTU
* Medidor de vazão e pressão com protcolo Modbus-RTU

Dessa forma pode se ler os variáveis elétricos dos medidores a cada 10 segundos passando valores de vazão, pressão, tensão, corrente, potência e frequencia da usina.

A frequencia de amostragen de 10 segundos é neste caso suficiente para o monitoramento da operação.

## 3.2. Implementação do Datasources no ScadaBR 


## 3.3. Implementação do Datapoint no ScadaBR 

## 3.4. Tela sinóptica no ScadaBR 


![](figuras/tela_scada00.jpg)


# 4. Central de monitoramento e acionamento remoto

O projeto de um central de monitoramento e acionamento remoto de uma micro unidade geradora de energia elétrica para localidades remotas. 
Este central tem como objetivo monitorar a geração de energia elétrica e sua qualidade (potência, energia, fator de potência, interrupções de fornecimento, etc), e mandar essas informações via internet para um computador central que serão intergradas num sistema Supervisório Control and Data Aquisition (Scada).
Este monitoramente está descrito no repositório em <https://github.com/rudivels/MicroHydro_Scada> 
[link](MicroHydro_Scada/README.md)

# 5. ScadaBR remoto

## 5.1. Comunicação via internet

No item 3.1 apresentou-se a ScadaBR lendo diretamente os medidores na planta. Entretanto, como entre o ScadaBR e o Multimedior há uma rede internet poderia-se implementar um link diretamente entre o sistema operacional lunix do Scada e o Central (Raspberry) e fazer um túnel para o Modbus-RTU. 

Entretanto a dificuldade neste sistema é que não temos um endereçamento IP fixo entre estes dois sistemas linux. Ou seja, há necessidade de um outro intermediário para estabelecer um canal de comunicação virtual entre os dois computadores.

Há diversos maneiras para implementar isso, e a opção escolhido foi o serviço de *Message Queuing Telemetry Transport (MQTT)*

Este sistema de comunicação usa o serviço de um intermediário ou *broker* para encaminhar as mensagens 

### 5.1.2. Assinante MQTT 

O cliente assinante ou *subscriber* permite a gente ler as mensagens que foram encaminhados pelo central local ao intermediário (*broker*). 
Há diversos nívels de serviço no MQTT com muitas funcionalidades. No nosso caso vamos pegar o caso mais simples sem nenhum mecanismo de verificação ou controle de entrega de mensagens.  

Usou-se como *broker* um servidor público aberto implementado pela <http://mqtt.eclipse.org>.

O ScadaBR não tem implementado o protocolo MQTT de forma nato no seu sistema. A maneira encontrada para fazer a leitura da mensagem MQTT pelo SacdaBR foi gravar este mensagem em disco.
A mensagem enviada pelo central de monitoramento tem o seguinte formato:

```
s=data_hora +";"+ frequencia +";"+ tensão_fase_A + ";" + tensão_fase_B +";"+ tensão_fase_C  +";"+ Corrente_A +";"+ Corrente_B +";"+ Corrente_C +";"+ Potencia_Ativa +";"+ Potencia_Reativa +";"+ Fator_potencia
publish.single("Topico", s ,hostname="mqtt.eclipse.org")
```
O string encaminhado tem este formato.

```
2020-05-25 00:07:00;60.0;220.0;220.0;220.0;10.0;11.0;15.0;2.20;2.30;0.72
```


No lado do receptor a mensagem é processado pela rotina.

```
msg = subscribe.simple("Topico", hostname="mqtt.eclipse.org")
s=msg.payload
print("%s "% (s))
```

cliente MQTT desenvolvido em python implementando o cliente mqtt subscriber e gravando o dados recebido num arquivo. 
O ScadaBR leia este arquivo por meio do 
`Data source`
`ASCII File Reader`

![](figuras/Tela_Ascii_File_Reader.jpg)

Observe que se usou o *regular expression (regex)* para ler o string alfanumérico de uma vez do MQTT e também consegiu-se obter o horário e data do evento. Entretanto, não foi possível separar os 9 valores embutidos no string usando regex. 
Gastei pelo menos uma 2 horas tentando forçar a barra com regex até me render e procurar outra solução. Uma ferramenta útil para experimentar com regex está no site <https://regex101.com/>.
Aparentemente a técnica de separação usando regex so funciona quando são até dois valores e o *timestamp*. 

Para distrinjar o dado recebido pelo MQTT use-se o `Meta Data Source` para processar o string que foi enviado pelo comando conforme tela a seguir:

![](figuras/Tela_Meta_data.jpg)

Com rotinas de tratamento de string conseguiu-se separar os argumentos do string do MQTT usando Javascript

Depois de ter deixado o ScadaBR rodar durante 2 dias num netbook linux 32bits, percebeu-se que o processador Java estava muito carregado no sistema operacional e tinha um atraso entre o processamento do *Ascii File Reader* e o *Meta Data Source*. Aparentemente tinha uma fila de processamento do *Meta Data Source* provocado pela chamada a rotina de Javascript que fez com que os valores na tela do data view eram atualizadas pelos menos alguns minutos depois da atualização do string proviniendo do Asci file reader. Pode ser que a fila de processamento tem um atraso que vai se acumulando na medida que a máquina fica ligada. Houve um ajuste de reduzir o temp de atualização para 10 segundos, pois o MQTT manda recebe os dados num intervalo de 10 segundos, somando com isso o atraso da leitura do barramento Modbus-RTU. 

### 5.1.2. Assinante MQTT com aviso de queda de comunicação

Uma das limitações deste sistema é que o Scada não é avisado quando há alguma falha na comunicação. O scada tem como dar algum alarme por meio de um evento para avisar que não houve a atualização no valor gravado no disco pelo assinante mqtt.
Ou seja, se num determinado intervalo de tempo nõ houve atualização do *data point*  o sistema gera um alarm. A tela a seguir mostrar como é configurado essa opção. Aqui o *Data point* mqtt_string do *Data source* microhydro1 é monitorada para ver se munda num intervalo de 2 minutos. Se não tiver mundança no data *source* o sistema gera um alarme.

![](figuras/Tela_evento_sem_comunicao.jpg)

Essa opção avisa o operador da falha de comunicação, mas não atualiza os últimos valores lidos. Deve ter uma maneira para avisar ao data source para voltar para um valor padrão em caso dessa falha. Entretanto não conseguimos descobrir como fazer isso no ScadaBR.
 
A opção encontrada foi implementar uma nova funcionalidade no assinante MQTT para ele monitorar o estado do *broker* e se a mensagem esperado não chegar em tempo ou o *broker* sair do o ScadaBR é avisado e toma os devidos providencias. 
Essa opção está mostrado no código a seguir 

```
# códgo assinante broker novo. 
# com aviso de erro de comunicação

from datetime import datetime
import paho.mqtt.subscribe as subscribe
import time
import sys

if (len(sys.argv))==2 :
	 print ("# logfile  = ", sys.argv[1])
	 logfile=True
else :
     logfile=False 

msg = subscribe.simple("ChapHydro", hostname="mqtt.eclipse.org")
s=msg.payload
print("%s "% (s))

if (logfile == True) :
     f = open(sys.argv[1],"w")
     f.write(s)
     f.write("\n")
     f.close()
 
print("Publicou dados ")


```



# 6. Controlador de carga 

Além disso, o central tem que perimitir a configuração e/ou reprogramação remota de um controlador de carga (load controller) dessa micro unidade geradora de energia elétrica. Este controlador de carga é implementado num hardware dedicado com microcontrolador Arduino que controle a rede trifásico de um pico central hidrelétrico por meio de um banco de triacs. ainda será detalhada em repostório próprio. Os detalhes dessa implementação estão no repositório <https://github.com/rudivels/Controlador_carga_3fas> [link](Controlador_Carga_TriFasico)


  

