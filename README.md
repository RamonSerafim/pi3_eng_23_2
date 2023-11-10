Curso Superior em Engenharia Eletrônica

Unidade Curricular: Projeto Integrador III

Professor: Daniel Lohmann e Robinson Pizzio

Florianópolis, Agosto de 2023

Aluno: Ramon Busiquia Serafim 
               

# Inversor Monofásico para carga RL



## Introdução

​		Esse relatório tem a finalidade de apresentar a contrução, análises, simulações e a construção de um inversor monofásico, na parte de controle do chaveamento, levando em consideração planilha de custo.



## Objetivos

Elaborar um relatório na qual conste projetar um inversor monofásico para carga RL operando com 3 diferendes modulações SPWM.



## Objetivos especificos

- Resultados teóricos, simulações, planilha de custo e etc;
- Requisitos do projeto escolhido;
- Aplicações do projeto escolhido;
- Resultados de Simulações;
- Esquemático do projeto;
- Projeto físico dos elementos do conversor escolhido:

  - Projeto do físico do indutor/transformador; 

  - Escolha dos capacitores do circuito; 

  - Escolha dos diodos do circuito; 

  - Projeto dos componentes associados ao funcionamento do CI; 

  - Escolha do Driver para comandar o(s) transistor(es); 

  - Escolha do transistor:

    - Cálculo de Perdas;

    - Escolha do Dissipador, se necessário;
- Liste de materiais (com part number) e Custo dos componentes; 

## Cronograma

|    Data    |                          Descrição                           |
| :--------: | :----------------------------------------------------------: |
| 28/07/2023 |              Apresentação da unidade curricular              |
|   04/08    |              Apresentação propostas de projeto               |
|   11/08    |              Apresentação propostas de projeto               |
|   18/08    |     Apresentação do cronograma e inicio da documentação      |
|   25/08    |  Apresentação do diagrama de blocos e requisitos do projeto  |
|   01/09    |        Desenvolvimento do projeto - Testes sinal SPWM        |
|   08/09    |        Desenvolvimento do projeto - Testes sinal SPWM        |
|   15/09    |                **Desenvolvimento do projeto**                |
|   22/09    |                **Desenvolvimento do projeto**                |
|   29/09    |                **Desenvolvimento do projeto**                |
|   06/10    | **Apresentação dos projetos em formato de prova de conceito** |
| 06/1010/10 |        Desenvolvimento do projeto - Testes sinal SPWM        |
|   20/10    |             **Desenvolvimento do projeto final**             |
|   27/10    |             **Desenvolvimento do projeto final**             |
|   03/11    |             **Desenvolvimento do projeto final**             |
|   10/11    |        **Apresentação do projeto final impementado**         |
|   17/11    |           **Testes de operação do projeto final.**           |
|   24/11    |           **Testes de operação do projeto final.**           |
|   01/12    |           **Testes de operação do projeto final.**           |
|   08/12    |     **Apresentação final da operação do projeto final.**     |



## Metodologia

~~pesquisa ou desenvolvimento~~

​		A partir do circuito, analisar adequadamente e fazer simulações via Software e analisar os resultados.

​		Para efetuar os cálculos dos componentes, foi utilizado o software SMath com o intuito de obter resultados mais rápido e precisos.

​		Após todos os componentes serem analisados, utilizamos o software de simulação PSIM para a geração de gráficos e análises pontuais do circuito.

​		Circuito representa em um banco de baterias com 50 VDC, ligada a um inversor, que conecta a um motor. Nosso projeto se encontra dentro do inversor, pois será a parte de alimentação para os drivers e conexões para o chaveamento.

## Requisitos do projeto Inversor Monofásico

- Proteções contra sobretensão na entrada;
- Tensão Nominal de Entrada: 50 VDC ;
- Saída(s): Tensão = --- VAC eficaz;
- Potência = -- W; 
- Prever circuito de grampeamento de tensão sobre o transistor (snubber); 
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

​		Podemos separar um optoacoplador em 2 partes, um LED infravermelho e um fototransistor. Quando o LED é acionado, a luz incide no transistor fazendo com que permita a condução de corrente.

### Transistor

### Driver

​		Um problema encontrado, será que os transistores na parte de cima do circuito terão com a fonte com tensão flutuante. Diferentemente dos transistores na parte de baixo, não possuem a referência diretamente conectada ao pino Source, com isso, precisamos de um sistema para garantir que o Vgs dos transistores não seja flutuante e sim o valor necessário para sua ativação.

​		Precisamos implementar esse sistema aos 4 transistores, a princípio seria somente necessário aos da parte de cima do circuito, porém, para maior segurança contra sobrecorrentes/curto-circuito e também para um melhor controle das chaves, colocaremos em todos. Com a utilização de drivers, eles possuem um delay interno na faixa de nano segundos e caso fosse implementado somente em nas chaves superiores poderia ocorrer algum erro de ativação devido a esse delay, sendo critico para o circuito.

​		Uma pergunta plausível de se fazer é como se funciona um driver, quais componentes são utilizados e como encontrar um para tal aplicação, contudo, será explicado a seguir.

​		Precisamos de uma fonte que alimente o driver, que usualmente se utiliza 15 V. Essa fonte é conectada a um CI oscilador e sua saída encontra um capacitor para tirar o offset dessa onda. Cada driver deve possuir sua "fonte" isolada, e o retificador isolador faz esse papel, retificando a onda quadrada encontramos 15VDC que será conectado a um optoacoplador, onde esse irá comandar a abertura ou fechamento dos mosfets. Portanto, o princípio de funcionamento do driver se resume a fonte + oscilador + capacitor + transformador isolador + retificador de meia onda + optoacoplador + mosfet.

<img src="C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\modelo antigo.jpg" alt="modelo antigo" style="zoom: 67%;" />
<img src="https://github.com/RamonSerafim/pi3_eng_23_2/tree/main/simulations/modelo antigo.jpg"/>
![modelo antigo](https://github.com/RamonSerafim/pi3_eng_23_2/blob/main/simulations/modelo%20antigo.JPG)

​		Conversado com o professor sobre o modelo da montagem, uma fora mais fácil de se montar esse esquemático foi com uma fonte já isolada presente no mercado. O circuito fica menor e será conectado diretamente no optoacoplador.

<img src="C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\novo modelo.jpg" alt="modelo" style="zoom:67%;" />

​		Algumas empresas já possuem drivers prontos para vender como a Texas e Mouser, porém, precisamos das fontes isoladas para cada um. A Supplier possui todos os componentes sendo vendido em módulos separados, driver único ou duplo (acionando 1 ou 2 mosfet), fonte isolada para até 2 drivers e retificadores isoladores separadamente.  Como estamos montando um projeto para testes, é benéfico possuir um inversor modular pois caso ocorra algum erro de funcionamento é possível descobrir facilmente onde está sendo gerado e consertá-lo. 

|            Componente            | Código Componente | Preço Supplier(R$/un) | Quantidade |  Total (R)  |
| :------------------------------: | :---------------: | :-------------------: | :--------: | :---------: |
|       Driver Duplo Isolado       |    DRO100D25A     |        640,00         |     2      |   1280,00   |
| Fonte Chaveada 2 canais Isolados |     DS320-08A     |        180,00         |     1      |   180,00    |
|     Transformador de  Pulso      |    TRM480D20A     |         55,00         |     2      |   110,00    |
|     **Compra total Drivers**     |         -         |           -           |     -      | **1570,00** |

  Afim de demonstrar a diferença ao construir o driver próprio, encontramos os componentes que constituem o driver na Mouser. Os itens listados são as principais peças para a sua montagem.
    

|            Componente            | Código Componente | Preço Mouser(dólar/un) | Quantidade | Total (dólar) |
| :------------------------------: | :---------------: | :--------------------: | :--------: | :-----------: |
|       Driver Duplo Isolado       |         -         |           -            |     -      |       -       |
| Fonte Chaveada 1 canais Isolados |         -         |           -            |     -      |       -       |
|     **Compra total Drivers**     |         -         |           -            |     -      |     **-**     |



### Gerador SPWM

​		PWM (Pulse Width Modulation) refere-se ao conceito de pulsar rapidamente um sinal digital. Além de várias outras aplicações, esta técnica de modulação pode ser utilizada para simular uma tensão estática variável e é comumente aplicada no controle de motores elétricos, aquecedores, LEDs ou luzes em diferentes intensidades ou frequências. 

​		O tempo de ativação é o tempo durante o qual a alimentação CC é aplicada à carga e o tempo de desativação é o período durante o qual a alimentação é desligada. Dada uma largura de banda suficiente, qualquer valor analógico pode ser codificado com PWM.

​		A forma mais simples de gerar um sinal PWM é utilizando uma onda triangular e uma fonte de tensão continua como referência. A imagem abaixo representa um sinal PWM com o tempo de ativação e desativação fixo, também chamado de duty cycle.

![sinal PWM](C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\sinal PWM.JPG)

​		A diferença para o sinal SPWM é que no lugar da tensão continua utilizamos um sinal senoidal como referência e uma onda triangular como moduladora. Ao realizar essa mudança, conseguimos encontrar na saída um sinal com duty cycle que varia de acordo com a comparação entre os sinais. 

<img src="C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\sinal SPWM.JPG" alt="sinal SPWM" style="zoom:67%;" />

​		A diferença entre os dois se da pela frequência de saída do SPWM se da pela senoide, que para utilização em motores se da em 60 Hz mas podendo ser alterado para a aplicação específica, já o PWM a frequência de saída se da pela frequência de comutação. PWM não necessita de filtros de saída.

​		Iremos utilizar um sinal SPWM nos gates dos mosfets para o funcionamento do inversor, existem duas maneiras para ser implementada, a primeira que seria montando por partes, utilizando CIs e geradores de ondas, ou então um microcontrolador. Para esse projeto utilizaremos o microcontrolador, pelo tempo de construção e pela afinidade utilizando o mesmo.

​		Para vizualizarmos se vai ser possível implementar, o software PSIM possui o componente "μController" mais conhecido como "C Block", onde conseguimos implementar todo o código do microcontrolador e verificar todas suas ondas geradas. O código para implementação pode ser encontrado aqui.

### Modulação SPWM

​		Uma alternativa para o esquema de chaveamento em onda quadrada é a modulação por largura de pulso senoidal. Essa apresenta valores menores de distorção harmônica total da corrente na carga, assim é mais fácil adequar o sistema à DHT necessária para aplicação. A desvantagem desse método é a complexidade de implementação.

​		Existe mais de um esquema de chavemeanto utilizando a modulação por largura de pulso senoidal, em seguida serão abordadas três deles: 

- Bipolar
- Unipolar
- Unipolar Alternativo

Todos os três dependem de uma senoide (referência) e uma onda triangular (portadora), e são tratados somente para a topologia estudada nesse projeto, o inversor de ponte completa. Os elementos do circuito serão tratados como estão na figura abaixo.

![Esquematico](C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\Esquematico.JPG)

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

![demo_bipolar](C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\demo_bipolar.png)


Para utilizar esse esquema no circuito basta fazer a seguinte alteração no script fornecido: ativar a opção BIPOLAR_SPWM e desative a opção ALT_TRI

### Unipolar

Nesse esquema a tensão de saída é chaveada de valor alto para zero e valor baixo para zero.

A lógica para as chaves S1,...S4 é a seguinte:

- S1 está ligada quando Vsen > Vtri
- S2 está ligada quando -Vsen < Vtri
- S3 está ligada quando -Vsen > Vtri
- S4 está ligada quando Vsen < Vtri

![demo_unipolar](C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\demo_unipolar.png)


Alterações para o script fornecido: Desative as opções BIPOLAR_SPWM e ALT_TRI


### Unipolar alternativo

Similar ao esquema unipolar, o comportamento da tensão de saída é o mesmo. No entanto, duas chaves operam em alta frequência (frequência da portadora) enquanto outras duas operam na frequência da referência. 

Lógica de chaveamento:

- S1 está ligada quando Vsen > Vtri
- S4 está ligada quando Vsen < Vtri  
- S2 está ligada quando Vsen > 0
- S3 está ligada quando Vsen < 0

![demo_unipolar_alternativa](C:\Users\ramon\Desktop\Ramon\facul\Projeto Integrador 3\demo_unipolar_alternativa.png)


Alterações para o script fornecido: Ativar a opção ALT_TRI e desative a opção BIPOLAR_SPWM 

### Comparando Esquemas de Chaveamento

### Resultados Gerais

## Próximos Passos

## Referências



explicar o micro controlador utilizado, timers, pwm, resolução...





Site compra componentes

https://br.mouser.com/



Gerador PWM

https://br.mouser.com/ProductDetail/onsemi/SG3525ANG?qs=xZq1yRCsb1dl9y1qJup1Qg%3D%3D

https://br.mouser.com/datasheet/2/308/1/SG3525A_D-2320132.pdf



Driver 

http://www.supplier.ind.br/produtos/drivers-para-igbt-e-mosfet/
https://br.mouser.com/ProductDetail/onsemi/NCP51560ABDWR2G?qs=vvQtp7zwQdNxehcZBK2Y8w%3D%3D



Mosfet

https://br.mouser.com/ProductDetail/Infineon-Technologies/IPA50R190CEXKSA2?qs=0DP5yvOrqYltp1qU%2FgDQGQ%3D%3D
https://br.mouser.com/datasheet/2/196/Infineon_IPA50R190CE_DS_v02_04_EN-3164043.pdf

Fonte isolada
http://www.supplier.ind.br/produtos/drivers-para-igbt-e-mosfet/
https://br.mouser.com/ProductDetail/RECOM-Power/R15P21503D?qs=gt1LBUVyoHkTyvT%2FUCCLXQ%3D%3D



referências

https://www.citisystems.com.br/pwm/

https://www2.dee.cefetmg.br/wp-content/uploads/sites/18/2017/11/TCC_2017_1_MPUlhoa.pdf
