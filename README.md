Curso Superior em Engenharia Eletrônica
Unidade Curricular: Projeto Integrador III
Professor: Daniel Lohmann e Robinson Pizzio
Florianópolis, Agosto de 2023
Aluno: Ramon Busiquia Serafim 
               

# Inversor Monofásico para carga RL



## Introdução

​		Esse relatório tem a finalidade de apresentar a construção, análises, simulações e a construção de um inversor monofásico, na parte de controle do chaveamento, levando em consideração planilha de custo.



## Objetivos

Elaborar um relatório na qual conste projetar um inversor monofásico para carga RL operando com 3 diferendes modulações SPWM.



## Objetivos especificos

- Resultados teóricos, simulações, planilha de custo e etc;
- Requisitos do projeto escolhido;
- Aplicações do projeto escolhido;
- Resultados de Simulações;
- Esquemático do projeto;
- Projeto físico dos elementos do conversor escolhido:

  - Projeto dos componentes associados ao funcionamento do CI; 

  - Escolha do Driver para comandar o(s) transistor(es); 

  - Escolha do transistor:

    - Cálculo de Perdas;

    - Escolha do Dissipador, se necessário;
- Liste de materiais (com part number) e Custo dos componentes; 

## Cronograma

|  **Data**  |                       **Descrição**                        |
| :--------: | :--------------------------------------------------------: |
| 28/07/2023 |             Apresentação da unidade curricular             |
|   04/08    |             Apresentação propostas de projeto              |
|   11/08    |             Apresentação propostas de projeto              |
|   18/08    |    Apresentação do cronograma e inicio da documentação     |
|   25/08    | Apresentação do diagrama de blocos e requisitos do projeto |
|   01/09    |       Desenvolvimento do projeto - Testes sinal SPWM       |
|   08/09    |       Desenvolvimento do projeto - Testes sinal SPWM       |
|   15/09    |                 Desenvolvimento do projeto                 |
|   22/09    |                 Desenvolvimento do projeto                 |
|   29/09    |                 Desenvolvimento do projeto                 |
|   06/10    | Apresentação dos projetos em formato de prova de conceito  |
|   10/10    |       Desenvolvimento do projeto - Testes sinal SPWM       |
|   20/10    |              Desenvolvimento do projeto final              |
|   27/10    |              Desenvolvimento do projeto final              |
|   03/11    |              Desenvolvimento do projeto final              |
|   10/11    |         Apresentação do projeto final implementado         |
|   17/11    |            Testes de operação do projeto final.            |
|   24/11    |            Testes de operação do projeto final.            |
|   01/12    |            Testes de operação do projeto final.            |
|   08/12    |      Apresentação final da operação do projeto final.      |



## Metodologia de desenvolvimento

​		A partir do circuito, analisar adequadamente e fazer simulações via Software e analisar os resultados.

​		Para efetuar os cálculos dos componentes, foi utilizado o software SMath com o intuito de obter resultados mais rápido e precisos.

​		Após todos os componentes serem analisados, utilizamos o software de simulação PSIM para a geração de gráficos e análises pontuais do circuito.

​		Circuito representa em um banco de baterias com 50 VDC, ligada a um inversor, que conecta a um motor. Nosso projeto se encontra dentro do inversor, pois será a parte de alimentação para os drivers e conexões para o chaveamento.



## Requisitos do projeto Inversor Monofásico

- Proteções contra sobretensão na entrada;
- Tensão Nominal de Entrada: 50 VDC ;
- Saída(s): Tensão = --- VAC eficaz;
- Potência = -- W; 
- Frequência operação (SPWM): 15 a 30 kHz;
- Frequência de saída: 60 Hz.
- Permitir 3 tipos de modulação

  - Unipolar;
  - Bipolar;
  - Unipolar alternativo;



## Inversor Monofásico

​		Inversores também são comumente chamados de conversores CC-CA, onde esses dispositivos são capazes de fornecer uma tesão/corrente alternada, com frequência e amplitude definidas pelo sistema de controle.

​		Os inversores são formados por pontes compostas de chaves semicondutoras que são acionadas por algum circuito de controle. Os inversores do tipo fonte de tensão são os mais conhecidos pela necessidade de potências elevadas, afim de acionar motores elétricos com maior potência.

​		Para o acionamento das chaves semicondutoras, é necessário um circuito de controle, onde esse determina a sua tensão de saída, frequência e amplitude de acordo com seu objetivo final. Comumente os semicondutores utilizados são transistores de efeito de campo, MOSFET, os de junção bipolar com porta isolada, IGBT, os de junção bipolar, TBJ, e  tiristores.

​		

## Componentes circuito de controle

### Optoacoplador

​		Um optoacoplador funciona como um botão ou um relé que pode ser acionado eletricamente. Porém, diferentemente dos relés, os circuitos são completamente isolados, assim o circuito que aciona o optoacoplador não é influenciado pelo circuito acionado.

​		O circuito interno do optoacoplador pode ser separado em 2 partes, um LED infravermelho e um fototransistor. Quando o LED é acionado, a luz incide no transistor fazendo com que permita a condução de corrente.

​		Para o nosso circuito, o sinal de entrada do optoacoplador será o sinal PWM, fazendo com que ative a chave somente no momento que que o sinal estiver alto.

### Driver

​		Um problema encontrado, será que os transistores na parte de cima do circuito terão com a fonte com tensão flutuante. Diferentemente dos transistores na parte de baixo, não possuem a referência diretamente conectada ao pino Source, com isso, precisamos de um sistema para garantir que o Vgs dos transistores não seja flutuante e sim o valor necessário para sua ativação.

​		Precisamos implementar esse sistema aos 4 transistores, a princípio seria somente necessário aos da parte de cima do circuito, porém, para maior segurança contra sobrecorrentes/curto-circuito e também para um melhor controle das chaves, colocaremos em todos. Com a utilização de drivers, eles possuem um delay interno na faixa de nano segundos e caso fosse implementado somente em nas chaves superiores poderia ocorrer algum erro de ativação devido a esse delay, sendo critico para o circuito.

​		Uma pergunta plausível de se fazer é como se funciona um driver, quais componentes são utilizados e como encontrar um para tal aplicação, contudo, será explicado a seguir.

​		Precisamos de uma fonte que alimente o driver, que usualmente se utiliza 15 V. Essa fonte é conectada a um CI oscilador e sua saída encontra um capacitor para tirar o offset dessa onda. Cada driver deve possuir sua "fonte" isolada, e o retificador isolador faz esse papel, retificando a onda quadrada encontramos 15VDC que será conectado a um optoacoplador, onde esse irá comandar a abertura ou fechamento dos mosfets. Portanto, o princípio de funcionamento do driver se resume a fonte + oscilador + capacitor + transformador isolador + retificador de meia onda + optoacoplador + mosfet.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/modelo%20antigo.JPG)

​		Conversado com o professor sobre o modelo da montagem, uma forma mais fácil de se montar esse esquemático foi utilizando uma fonte já isolada presente no mercado. O circuito fica menor e será conectado diretamente no driver com optoacoplador.





# FOTO MODELO NOVO




​		Algumas empresas já possuem drivers prontos para vender como a Texas e Mouser, porém, precisamos das fontes isoladas para cada um. A Supplier possui todos os componentes sendo vendido em módulos separados, driver único ou duplo (acionando 1 ou 2 mosfet), fonte isolada para até 2 drivers e retificadores isoladores separadamente.  Como estamos montando um projeto para testes, é benéfico possuir um inversor modular pois caso ocorra algum erro de funcionamento é possível descobrir facilmente onde está sendo gerado e consertá-lo. 

|            Componente            | Código Componente | Preço Supplier(R$/un) | Quantidade | Total (Reais) |
| :------------------------------: | :---------------: | :-------------------: | :--------: | :-----------: |
|       Driver Duplo Isolado       |    DRO100D25A     |        640,00         |     2      |    1280,00    |
| Fonte Chaveada 2 canais Isolados |     DS320-08A     |        180,00         |     1      |    180,00     |
|     Transformador de  Pulso      |    TRM480D20A     |         55,00         |     2      |    110,00     |
|     **Compra total Drivers**     |         -         |           -           |     -      |  **1570,00**  |

​		Para este projeto, iremos construir nosso próprio driver isolado, que possui optoacoplador interno, juntamente com uma fonte já isolada para diminuir o tamanho da placa e ficar modular. Encontramos os componentes que constituem o driver na Mouser. Os itens listados são as principais peças para a sua montagem.

|           Componente           | Código Componente | Preço Mouser(Dólar/un) | Quantidade | Total (Dólar) |
| :----------------------------: | :---------------: | :--------------------: | :--------: | :-----------: |
|         Driver Isolado         |   FOD3182TSR2V    |          3,10          |     4      |     12,40     |
| Fonte Chaveada 1 canal Isolado |    R15P21503D     |         10,04          |     4      |     40,16     |
|    **Compra total Drivers**    |         -         |           -            |     -      |   **52,56**   |

​		Com a cotação do dólar hoje (19/12/2023) em R$4,87, a construção dos 4 drivers isolados fica em torno de R$256,00.

​		A fonte isolada precisa de alimentação linear entre +12 até +24V, como o componente usado já é isolante, precisamos apenas de uma fonte externa para alimentar todos os drivers. Para essa função utilizamos uma fonte chaveada compacta com tensões de entrada entre 100 e 240V AC e é capaz de fornecer até 250 mA em uma tensão de 12 +/- 0.1V, sendo facilmente encontrada no mercado nacional.

|           Componente           | Código Componente | Preço MultComercial(R$/un) | Quantidade | Total (Reais) |
| :----------------------------: | :---------------: | :------------------------: | :--------: | :-----------: |
| Fonte Chaveada 1 canal Isolado |     HLK-PM12      |           42,00            |     1      |     42,00     |
|    **Compra total Drivers**    |         -         |             -              |     -      |   **42,00**   |



### Transistor

​		O transistor repesenta as chaves para o circuito, será por ele que a tensão do banco DC passará. Precisamos encontrar um transistor que suporte a tensão desejada e de preferência com poucas perdas. Utilizamos o IRF540 pois possui tensão VDS de 100 V, sendo super dimensionado para a aplicação, afim de possuir uma margem para futuras aplicações e encontramos com facilidade no IFSC câmpus Florianópolis e no mercado nacional. 

​		Possui um Rise Time de 45 ns e Fall time de 20 ns, esses dados juntamente com a frequência de operação determinam as perdas de comutação e condução do Mosfet, com valores baixos, as perdas serão menores.

|        Componente        | Código Componente | Preço Poesi(R$/un) | Quantidade | Total (Reais) |
| :----------------------: | :---------------: | :----------------: | :--------: | :-----------: |
|    Transistor Mosfet     |      IRF540       |        5,07        |     4      |     20,21     |
| **Compra total Drivers** |         -         |         -          |     -      |     20,21     |



### Gerador SPWM

​		PWM (Pulse Width Modulation) refere-se ao conceito de pulsar rapidamente um sinal digital. Além de várias outras aplicações, esta técnica de modulação pode ser utilizada para simular uma tensão estática variável e é comumente aplicada no controle de motores elétricos, aquecedores, LEDs ou luzes em diferentes intensidades ou frequências. 

​		O tempo de ativação é o tempo durante o qual a alimentação CC é aplicada à carga e o tempo de desativação é o período durante o qual a alimentação é desligada. Dada uma largura de banda suficiente, qualquer valor analógico pode ser codificado com PWM.

​		A forma mais simples de gerar um sinal PWM é utilizando uma onda triangular e uma fonte de tensão continua como referência. A imagem abaixo representa um sinal PWM com o tempo de ativação e desativação fixo, também chamado de duty cycle.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/sinal%20PWM.JPG)

​		A diferença para o sinal SPWM é que no lugar da tensão continua utilizamos um sinal senoidal como referência e uma onda triangular como moduladora. Ao realizar essa mudança, conseguimos encontrar na saída um sinal com duty cycle que varia de acordo com a comparação entre os sinais. 

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/sinal%20SPWM.JPG)

​		A diferença entre os dois se da pela frequência de saída do SPWM se da pela senoide, que para utilização em motores se da em 60 Hz mas podendo ser alterado para a aplicação específica, já o PWM a frequência de saída se da pela frequência de comutação. PWM não necessita de filtros de saída.

​		Iremos utilizar um sinal SPWM nos gates dos mosfets para o funcionamento do inversor, existem duas maneiras para ser implementada, a primeira que seria montando por partes, utilizando CIs e geradores de ondas, ou então um microcontrolador. Para esse projeto utilizaremos o microcontrolador, pelo tempo de construção e pela afinidade utilizando o mesmo.

​		Para vizualizarmos se vai ser possível implementar, o software PSIM possui o componente "μController" mais conhecido como "C Block", onde conseguimos implementar todo o código do microcontrolador e verificar todas suas ondas geradas. O código para implementação pode ser encontrado aqui.



### Microcontrolador

explicar o micro controlador utilizado, timers, pwm, resolução...



### Modulação SPWM

​		Uma alternativa para o esquema de chaveamento em onda quadrada é a modulação por largura de pulso senoidal. Essa apresenta valores menores de distorção harmônica total da corrente na carga, assim é mais fácil adequar o sistema à DHT necessária para aplicação. A desvantagem desse método é a complexidade de implementação.

​		Existe mais de um esquema de chavemeanto utilizando a modulação por largura de pulso senoidal, em seguida serão abordadas três deles: 

- Bipolar
- Unipolar
- Unipolar Alternativo

Todos os três dependem de uma senoide (referência) e uma onda triangular (portadora), e são tratados somente para a topologia estudada nesse projeto, o inversor de ponte completa. Os elementos do circuito serão tratados como estão na figura abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Esquematico.JPG)

O conceito de taxa de modulação da frequência (mf) será mencionado, essa é a relação entre as frequências da portadora e da referência:
$$
mf = {f_{portadora} \over f_{referência}} = {f_{tri} \over f_{sen}}
$$
 ~~mf = {f_{portadora} \over f_{referência}} = {f_{tri} \over f_{sen}}~~ 

### Bipolar

Nesse esquema a tensão de saída do circuito alterna entre positivo e negativo do barramento DC, por isso é chamado de bipolar.

A lógica para as chaves S1,...S4 é a seguinte:

- S1 e S2 estão ligadas quando Vsen > Vtri  (Vout = +Vcc)
- S3 e S4 estão ligadas quando Vsen < Vtri  (Vout = -Vcc)

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/demo_bipolar.png)


Para utilizar esse esquema no circuito basta fazer a seguinte alteração no script fornecido: ativar a opção BIPOLAR_SPWM e desative a opção ALT_TRI

### Unipolar

Nesse esquema a tensão de saída é chaveada de valor alto para zero e valor baixo para zero.

A lógica para as chaves S1,...S4 é a seguinte:

- S1 está ligada quando Vsen > Vtri
- S2 está ligada quando -Vsen < Vtri
- S3 está ligada quando -Vsen > Vtri
- S4 está ligada quando Vsen < Vtri

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/demo_unipolar.png)



Alterações para o script fornecido: Desative as opções BIPOLAR_SPWM e ALT_TRI


### Unipolar alternativo

Similar ao esquema unipolar, o comportamento da tensão de saída é o mesmo. No entanto, duas chaves operam em alta frequência (frequência da portadora) enquanto outras duas operam na frequência da referência. 

Lógica de chaveamento:

- S1 está ligada quando Vsen > Vtri
- S4 está ligada quando Vsen < Vtri  
- S2 está ligada quando Vsen > 0
- S3 está ligada quando Vsen < 0

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/demo_unipolar_alternativa.png)

Alterações para o script fornecido: Ativar a opção ALT_TRI e desative a opção BIPOLAR_SPWM 



## Montagem Física

​		Esse tópico abordará a montagem dos circuitos mencionados anteriormente em Placas de Circuito Impresso (PCI), feitas no Laboratório de Protótipos do IFSC câmpus Florianópolis.

​		A construção dos layouts foi utilizado o software KiCad, um aplicativo Open Source que permite construção de placa e sua visualização 3D.

### Drivers

​		Para a construção do Driver precisamos entender de uma coisa, a alimentação 12 V será feita por uma alimentação externa, portanto terá outra referência, após passar pela fonte chaveada isolada a referência será do sinal PWM. O esquemático para o driver será apresentado abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Esquematico_driver.PNG)

​		Afim de deixar o circuito de acionamento compacto, utilizamos todos os componentes SMD, diminuindo o tamanho final. Abaixo será apresentado o layout da placa.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Layout_driver.PNG)

​		A placa utilizada foi de face simples, precisando colocar um jumper manualmente. Abaixo será apresentado o driver já montado.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/driver_montado.PNG)

​		Para melhor suporte na placa de potencia, utilizamos barra pino duplo.

### Placa Potência

​		Para a Placa de potência, precisamos separar em 3 referencias diferentes, a primeira sendo da alimentação dos drivers, a segunda sendo do micro controlador com seu sinal SPWM e a terceira sendo o barramento DC com os mosfets. O esquemático será apresentado abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Esquematico_Potencia.PNG)


​		A placa inicial de potência (versão 1) foi encontrado erros de posição dos barra pinos e em relação a referência, mesmo com adaptação efetuamos os testes com essa versão apresentada abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Layout_potencia_V1.PNG)


​		

​		Com o intuito de arrumar os erros anteriores para futuros projetos, ajustamos os defeitos de layout e a placa de potência final (versão 2) será apresentado abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/Layout_potencia.PNG)


​	A placa utilizada foi de face simples, precisando colocar jumpers manualmente. Abaixo será apresentado a placa de potência montada (versão 1).

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/potencia_montada.PNG)




### Montagem Final

​		Com as placas prontas, a montagem foi feita e é demonstrada nas imagens abaixo.
![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/placa_montada_horizontal.PNG)
![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/placa_montada_vertical.PNG)



## Resultados Gerais

​		Esse tópico abordará os resultados do projeto com sinais visualizados pelo osciloscópio.

##### Sinal SPWM

​		A primeira vista, seria simples a criação do SPWM com o STM32F103C8 com seu modelo de comparação interno, porém, se tornou dificultosa e pouco eficiente. A frequência de comparação seria muito baixa não sendo utilizável na topologia do circuito, portanto, passamos a utilizar um sinal PWM para verificar o funcionamento dos drivers e da ponto H (inversor monofásico).



##### Sinal PWM

​		Para certificar o sinal utilizado, visualizamos o sinal PWM e seu complementar, em primeiro momento possuindo uma frequência de 5 kHz e não podendo serem ativos ao mesmo momento. Utilizamos um dead-time de 1 us para este modelo, muito acima do necessário pois somando o rise time e fall time do mosfet precisaríamos de um dead-time de no mínimo 65 ns, mas para uma melhor segurança, utilizamos 1 us.

​		A figura abaixo demonstra como ficou os sinais PWM juntamente com a frequência no canto inferior direito.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/sinal_pwm.PNG)

​		O sinal permanece constante e com uma frequência de 5,017 kHz, validando o sinal.



##### Drivers

​		Começaremos visualizando a saída dos drivers separadamente, afim de encontrar o valor saída no Gate +15 V e -3 V (sinal da fonte chaveada isolada).

​		Aplicando o sinal PWM no driver com a alimentação +12 V, conseguimos o sinal de saída em +16 V e -3 V, sendo o esperado para a aplicação do projeto. A figura abaixo demonstra a saída do driver pelo osciloscópio.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/sinal_driver.PNG)

​		O mesmo teste foi realizado para os 4 drivers e todos apresentaram a mesma forma de onda, validando que a saída está correta e ativará os mosfets.



##### Ponte H

​		Para testar o funcionamento e verificar se possui algum erro de construção, utilizamos uma tensão no barramento DC de 25 V e apenas um resistor com potência máxima de 3 W.

​		Como foi dito no tópico de construção da placa de potência, houve alguns erros primeiramente e depois os próprios foram consertados, porém, há um erro na placa proveniente dos ajustes fazendo com que não funcione perfeitamente.

​		Vamos visualizar a tensão de cada braço do conversor,  o primeiro braço do inversor será demonstrado na imagem abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/braco_positivo.PNG)

​		Podemos visualizar que está correto, como o barramento DC é de 25 V, a saída está entre 0 e +25 V pois a referência está sendo o barramento DC.

​		Agora vamos verificar o segundo braço do inversor, que será apresentado na imagem abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/braco_negativo.PNG)

​		Como podemos visualizar a tensão está entre -12,8 V e 50,4 V, sendo que o correto seria estar com 0 e +25 V pois a referência de medida está sendo o barramento DC. Esse erro é proveniente da montagem da placa de potência, como foi a versão 1 adaptada com jumpers, pode ser uma conexão incorreta ocasionando esse erro. é desconsiderado erro nos drivers pois eles foram testados anteriormente e posteriormente e não foi apresentado erro.

​		Agora utilizando a função MATH do próprio osciloscópio conseguimos verificar a diferença entre os dois braços, sendo apresentado abaixo.

![](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/saida_inversor.PNG)

​		Visualizando o resultado do inversor, a tensão de saída está entre -37,6 V e 75,2 V, diferente do esperado que seria -25 V e +25 V, isso ocorre pois um dos braços não está funcionando corretamente e deve ser ajustado nas próximas aplicações.



## Considerações Finais

​		A partir dos testes e dos resultados apresentados, podemos concluir que a topologia demonstrada acima funciona. Os erros apresentados foram devidos a placa de potência não estar devidamente construída pois possuía muitas adaptações. Com a versão 2 da placa de potência o resultado ficará muito próximo ao esperado, sem erros.

​		Os drivers funcionam corretamente, acionando os mosfets de forma adequada e com boa qualidade sendo isolados.



## Próximos Passos

​		Esse tópico abordará algumas melhorias para o circuito testado e apresentado.



#### Melhorias:

* Utilizar a versão 2 da placa de potência apresentada
* Implementação do SPWM, verificando outra maneira de ser implementada
* Fonte 3.3V para micro controlador
* Borne para saída do inversor, podendo ajustar o valor da carga externamente



## Referências

Site compra componentes

https://br.mouser.com/

https://proesi.com.br/

https://www.multcomercial.com.br/



Gerador PWM

https://br.mouser.com/ProductDetail/onsemi/SG3525ANG?qs=xZq1yRCsb1dl9y1qJup1Qg%3D%3D

https://br.mouser.com/datasheet/2/308/1/SG3525A_D-2320132.pdf



Driver 

http://www.supplier.ind.br/produtos/drivers-para-igbt-e-mosfet/
https://br.mouser.com/ProductDetail/onsemi-Fairchild/FOD3182TSR2V?qs=iQhsftLtcNTyNCxiozQbZg%3D%3D



Mosfet

https://br.mouser.com/ProductDetail/STMicroelectronics/IRF540?qs=FOlmdCx%252BAA2M1uLloR9EEQ%3D%3D



Fonte isolada
http://www.supplier.ind.br/produtos/drivers-para-igbt-e-mosfet/
https://br.mouser.com/ProductDetail/RECOM-Power/R15P21503D?qs=gt1LBUVyoHkTyvT%2FUCCLXQ%3D%3D
