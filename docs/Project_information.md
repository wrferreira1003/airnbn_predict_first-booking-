# airnbn_predict_first-booking
==============================

# Project in progress...

Projeto de Previsão do primeiro destino que um novo usuario irá escolher.


## Contextualização:

Os dados do projeto foram obtidos do kaggle, do desafio "airnbn_predict_first-booking".

O contexto do negócio é fictício, porem todo o planejamento e desenvolvimento da solução esta sendo realizado seguindo todos os passos de um projeto real para o mercado de trabalho.

Todo o projeto é desenvolvido utilizando a metodologia CRISP-DS

# Entendendo o problema

- Objetivo do problema: Precisamos prever qual será o primeiro destino que um novo usuario irá escolher.
- Tipo de Negocio Airbnb: Marketplace (Conecta pessoas que oferecem acomodações, com pessoas que estão procurando acomodações)
- Oferta: Pessoas oferencendo acomodações (Tamanho do portfolio, Diversidade/densidade de portfolio, preço medio)
- Demanda: Pessoas procurando acomodações (Numero de Usuarios, LTV(Lifitime value), CAC(Client Acquisition cost))
- Gross Revenue ( FEE * Numero de clientes) - CAC

# Informações das Features Tabela train_user

|Feature Name| Information|
|----------------|:---------------:|
|id:                         |user id
|date_account_created:       |the date of account creation
|timestamp_first_active:     |timestamp of the first activity, note that it can be earlier than date_account_created or date_first_booking because a user can search before signing up
|date_first_booking:         |date of first booking
|gender                      |
|age                         |     
|signup_method               |
|signup_flow:                |the page a user came to signup up from
|language:                   |international language preference
|affiliate_channel:          |what kind of paid marketing
|affiliate_provider:         |where the marketing is e.g. google, craigslist, other
|first_affiliate_tracked:    |whats the first marketing the user interacted with before the signing up
|signup_app                  |
|first_device_type           |
|first_browser               |
|country_destination:        |this is the target variable you are to predict

|Feature Name| Information|
|----------------|:---------------:|
|id:                         |ID do Usuario
|date_account_created:       |Data da Criação da Conta
|timestamp_first_active:     |Data do cadastro, note que pode ser anterior à data de criação da conta ou à data da primeira reserva porque um utilizador pode pesquisar antes de se inscrever
|date_first_booking:         |data da primeira reserva
|gender                      |Sexo
|age                         |Idade 
|signup_method               |Metodo de inscrição
|signup_flow:                |fluxo de inscrição: a página de onde um utilizador veio para se inscrever
|language:                   |Preferencia linguistica internacional
|affiliate_channel:          |canal afiliado: que tipo de marketing pago
|affiliate_provider:         |fornecedor afiliado: onde o marketing é, por exemplo, google, craigslist, outro
|first_affiliate_tracked:    |primeira afiliação rastreada: qual foi o primeiro marketing com que o utilizador interagiu antes da inscrição
|signup_app                  |Aplicativo de inscrição
|first_device_type           |Primeiro tipo de dispositivo
|first_browser               |Primeiro nagevagor
|country_destination:        |Destino do pai:Variavel alvo que deve prever

# Informações das Features Tabela session
|Feature Name| Information|
|----------------|:---------------:|
|user_id:           | to be joined with the column 'id' in users table
|Id in users Table  | Tabela de utilizadores
|action             | Açao
|action_type        | Tipo de ação
|action_detail      | Detalhe da ação
|device_type        | Tipo de dispositivo
|secs_elapsed       | segundos

# Criação das Hipóteses

- H1 - Escolha do destino pela estação do ano
- H2 - Escolha do destino em relação aos Feriados 
- H3 - Escolha do Destino em relação a promoção
- H4 - Escolha do Destino em relação ao Sexo
- H5 - Escolha do destino em relação a idade
- H6 - A maioria dos clientes escolhem UK, tentar identificar por qual motivo.
- H7 - Data da primeira Reserva, qual periodo do ano, qual estção e lugar escolhido.
- H8 - Proporção do sexo e idade que acessa o site.
- H9 - Qual o metodo de incrição mais utilizado com os destino escolhido, será que o metodo pode inflienciar na escolha do local
- H10- Fluxo de inscrição, A pagina acessada antes de vim para a pagina do airbnb conseguimos identificar se influencia na escolha do destino
- H11- Tipo de preferencia linguistica influencia na escolha do destino
- H12- Fornecedor afiliado, não pode ser de algum destino e de alguma forma pode influenciar a decisão do cliente
- H13- 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Ciclo001 - End to End

No primeiro Ciclo do crisp (End to End) foi criado todo o pipeline do projeto, e consegui identificar que existe um grande desbalanceamento na nossa variavel respota, e nosso modelos inicial teve uma performance de 0.09 (Balanced Accuracy: 0.09)

Porque utilizei Balanced Accuracy: Uma metrica para classes desbalanceada, pois como ela vai da uma media muito alto para a classe majoritaria e uma media muito baixa para as demais classe, chegando em um resultado final baixo, como deve ser nesses casos de classe desbalanceada.

### Conclusão do primeiro ciclo:

Não posso avaliar a matriz de confusão, onde ficou bem claro o desbalanceamento onde o modelo fez previsão na classe majoritária e arrumar o desbalanceamento atraves de tecnicas estatisticas, precisamos antes 

seguir alguns passos:
- Criar Feature
- Limpar o ruido
- e depois sim realizar o balanceamento

Fazendo o balanceamento com os dados sujos ou sem nenhuma features criada para representar o modelo o Balanceamento vai piorar ainda mais o problema.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Ciclo002 - Imbalanced Metrics

Neste ciclo trabalhei com as metricas dos modelos, pois conforme o ultimo ciclo, foi identificado que temos as classes bem desbalanceadas e a ideia do ciclo anterior foi apenas de montar todos os pipeline do projeto, ignorano sujeira nos dados e uma analise mais detalhada do mesmo que iremos realizar mais para frente, o objetivo foi identificar que temos classes desbalanceada e decidir quais metricas mais se ajustam a realidade dos dados. Neste caso decidi utilizar o Balanced Accuracy e Kappa Score que explico no detalhe abaixo.

Balanced Accuracy - Essa metrica pega a media das acurácias de cada classe, a vantagem da metrica é que ela vai da sempre um valor baixo, pois algumas das condições vai esta muilto alto e as outras classes muito baixo, com isso conseguimos penalizar a classe majoritária e temo um resultado mais fiel a realidade.

Kappa Score - Essa metrica medi o nivel de acordo entre 2 avaliadores, entende-se como avaliador o modelo que faz a predição e o outro avaliador seria a classe real. A formula do Kappa score da a probabilidade de haver um acordo entre dois estimadores e esse acordo seja maior do que um acordo aleatório. Enquanto um acordo entre dois estimadores é melhor do que se os dois jogasse uma moeda, temos uma garantia estatistica que o resultado será melhor do que um modelo aleatório.

### Conclusão do primeiro ciclo:
Neste ciclo o bjetivo foi alcançado com a implementação das metricas.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Ciclo003 - Cross_validation

A intenção deste ciclo foi a criação apenas do pipeline do cross validation, pois entendo que este processo evita termos o problema do viés de seleção, onde no processo de selecionar 80% para treino e 20% para teste conforme feito no ciclo passado, podemos ter sorte de selecionar uma boa amostra dos dados de teste ou vise e versa. Se não tratarmos o vies de seleção podemos esta vendo a performance do modelo errado ou podemos estar inputando nossos axismo dentro dos dados, fazendo que o modelo aprenda o que queremos e não o que deveria realmente aprender.
Com a criação do cross validation, amostramos o conjunto de dados mais vezes, garantindo o aprendizado de todos os padrão dos dados. 

### Conclusão do ciclo:
Apos rodar o cross validation tivemos ainda uma performance muito ruim do modelo, este resultando ja era esperado pois o desenvolvimento deste ciclo foi apenas para deixar o pipeline pronto, e nos demais ciclos estarei trabalhando na limpeza dos dados, criação de features e no balanceamento. Acredito que teremos uma boa melhora do modelo apos essas etapas.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Ciclo004 - Feature_Engineering

Neste ciclo iniciamos todas a parte de tratamento dos dados, vou detalhar abaixo o que foi feito e o motivo de cada decisão.

## 1 - Data Description

Nesta estapa verifico o o resumo dos dados, dimensão dos dados, o tipo de variaveis que temos e faço a checagem se temos NA nos dados.

No caso dos dados em questão tivemos que tomar algumas decisões referente aos dados faltantes, detalho abaixo o motivo para cada coluna.

## 1.1 Treatment NA

### Coluna: date_first_booking (Primeiro book do cliente)

Nesta coluna, tinhamos quase 60% de dados faltante, e os dados representava 100 de uma classe, onde precisei analisar a fundo para conseguir substituir por alguma data, não podia perder 60% dos dados, faria muita falta. Analisando a relação da coluna com as classes, identifiquei que a maioria que não tinha destino definido não teria a data da reserva, fazendo todo sentido. Para este caso se tivesse trabalhando para a Airbnb eu colocaria a data do dia atual, pois todos os dias os dados seria atualizado para a data atual, pois quando o cliente entrou no site até hoje teria x dias que ele ainda não fez o book, e dessa forma seria calculado essa quantidade de dias como features, como esses dados não estão atualizados, irei pegar a ultima data que temos de informação na coluna e adicionar para os dados faltante.

### Coluna Age (Idade)

Nesta coluna tinhamos 41% de dados faltantes, fiz a relação das idades com a classe e tinhamos os dados bem distribuidos de 20 a 65 anos, e umas idades estranha que iremos tratar mais a frente, o foco aqui era resolver o problema dos dados faltantes. Como as idades estava distribuidos tinhamos quase uma distribuição normal, neste caso podemos substituir pela media, pois podemos afirmar que substituindo pela media não estamos colocando viés nos dados. Se os dados tem uma distribuição normal quer dizer que podemos representar ele por uma media e desvio padrão.

### Coluna first_affiliate_tracked (primeira afiliação rastreada: qual foi o primeiro marketing com que o utilizador interagiu antes da inscrição)

Nesta coluna temos apenas 3% de dados faltantes, neste caso por ser dados categoricos, prefiro jogar fora do que tentar substituir e acabar inputando um viés nos dados.

### sessions.csv (data1)

Para a nossa segunda base de dados, exclui todos os dados faltantes, pois tenho mais de 1 milhão de dados e um percentual muito abaixo de dados faltantes. 


Dessa forma finalizamos a etapa de tratamento dos NAs.

## Change Data Type

Nesta estapa, apenas algumas transformações de tipo de dados.

## 2 Descriptive Statistics

### 2.1 - Variaveis numericas

### Coluna AGE
Avaliando esta coluna notei inconsistencia nos dados, pois tinhamos pessoas com idade minima de 1 ano e maxima 2014, claramente erros de digitação. Primeiramente fiz uma analise dos clientes acima de 80 anos, como que esses clientes estavam distribuidos em relação a variavel resposta, notei que seguia a mesma distribuição desbalanceada da variavel resposta, então faz sentido manter uma faixa de idade acima de 80 anos, decidi fica com os dados onde a idade minima seria 15 anos e a idade maxima 120 anos.

### secs_elapsed
Essa feature nos tras as informações de quanto tempo o cliente permaneceu no site, estranhamente temos tempo = 0, desta forma limpamos os dados que tinha valor 0.

### 2.2 Variaveis categoricas
A maioria das features são categoricos, desta forma fiz avaliação de cada features utilizando sweetviz, com foco na quantidade de categoria de cada variavel, algumas features chama atençao com mais de 50 categoria, onde posso ter problemas na hora da preparação dos dados, pois dependendo da tecnica aplicada posso ter problemas de dimensionalidade dos dados, uma forma de tentar diminuir é verificando a correção dessas variavel e onde tive uma correlação acima de 0.6 posso escolher a variavel com maior numero de categoria e retirar ela dos dados. Nessa etapa a intenção é apenas identificar essas features e mais a frente iremos executar os filtros necessarios.

Resumo das correlações:

Temos algumas correlações interrantes:

Dados dos Usuarios:

affiliate_channel x affiliate_provider = correlação de 0.62
first_device_type x first_browser = correlação de 0.63
first_device_type x signup_app = 0.65

Dados das sessions:

action x action_type = correlação de 0.95
action_detail x action_type = correlação de 0.98

Lembrando que acima de 0.60 ja consideramos uma correlação forte e podemos escolher excluir umas das variaveis, de preferencia para este caso a que tiver a maior quantidade de categorias.

### Conclusão do ciclo:

Neste ciclo foi efetuado o tratamento dos NAs, onde tomei algumas decisões para cada features utilizando algumas tecnicas de negócio e estatisticas para identificar a melhor forma de substituir os deletar os dados faltantes. Fiz a analise Estatistica das variaveis numericas e categoricas. Na analise da coluna AGE identifiquei inconsistencia e com uma investigação mais profunda defini a faixa de idade que irei trabalhar. 
En relação as features categoricas, fiz uma verificação da quantidade de categoria para cada variaveis e as correlações entre ela, onde nos proximo ciclos irei retirar do dataset essas variavei que tem uma alta correlação e com uma quantidade grande de categorias, tentanto evitar a maldição da dimensionalidade.
Finalizando rodei novamente o modelo e tive uma leve melhora na peformace dele:

Accuracy:          0.6234662019893995
Balanced Accuracy: 0.10740227055978153
Kappa Score:       0.2404154316603052

# Ciclo005 - Balanced Dataset

Neste ciclo foi desenvolvido o Pipelane do balanceamento dos dados. 
Lembrando que não podemos julgar o modelo antes de cumprirmos todas as etapas necessária para melhorar os dados:
Limpeza  dos dados, Susbstituição dos dados Faltantes, Criação das features para modelar o fenomeno, Desbalanceamento dos dados, escala dos dados e Seleção de Features.
Outro problema é que pode acontecer que o modelo que estamos usando tem um viés muito diferente do dados e com isso o modelo não consegue performar bem para esses tipos de dados.

Para balancear os dados utilizei a união dos metodos Smote-Tomek Links.
O Smote gera exemplos com base na distância de cada dado (Geralmente usando a distancia euclidiana) e os vizinhos mais proximos da classe minoritária, portanto, os exemplos gerados são diferentes da classe majoritária original. Esse método é eficaz porque os dados sintéticos gerados são relativamente próximos do espaço de recusros na classe majoritária, adicionando assim novas "informações" aos dados.
Tomek links usa a regra para selecionar o par de observações (Digamos, a e b) que são atendidos nessas propriedades:
1. O vizinho mais proximo da observação a e b.
2. O vizinho mais proximo da observação b é a.
3. As observações a e b pertencem a uma classe diferente. Ou seja, a e b pertencem à classe minoritária e majoritária (Ou vice-versa), respectivamente.

A União dos dois metodos combina a capacidade do SMOTE de gerar dados sintéticos para a classe minoritária e a capacidade dos links Tomek de remover os dados indentificados como links tomek da classe majoritária (ou seja, amostras de dados da classe majoritária mais proxima com os dados da classe minoritária).

Apos o processo de balanceamento tivemos uma pequena melhora no modelo, ainda utilizando REDE Neural, mesmo sabendo que não parece ser uma boa escolha de modelo para esse problema de negócio, mas a intenção é seguir todos os passos na transformação dos dados e quando todo processo tiver pronto e verificar outros tipos de modelo que melhor performance com o problema de negócio.

Accuracy:           0.19084187478183606
Balanced Accuracy:  0.16665973863452888
Kappa Score:        0.10566975266472478

# Ciclo006 - Exploratory Data Analysis

Objetivo deste ciclo é ganhar experiencia de negócio atraves dos dados, Como cientista de dados na maioria das vezes não estamos na operação do dia dia das empresas, neste caso não sabemos as metricas, como todo negócio funciona, a analise dos dados seria a melhor forma de enchergar o modelo de negócio da empresa do ponto de vista do dados. 
A analise de dados é a melhor forma de entender o negocio que estamos inseridos.
    Gerar Insights para o time de Negocio;
    Avaliar i impacto das features sobre o fenomeno.

# Ciclo007 - Feature Selection

"A explicação mais simples sobre um fenomeno observado, deveria prevalecer sobre explicações mais complexas"

Quanto mais features temos, mais espaço vai sendo criado e mais esparço os dados vão ficando. Chegando em um ponto que já não temos mais a representação do fenomeno original.
Para este caso usamos o algoritmo boruta para selecionar as principais features do projeto comparando com um modelo de arvore. 
Com as features selecionada tivemos o seguinte resultado da NLP:

Accuracy:          0.36634087519436426
Balanced Accuracy: 0.36500792894874645
Kappa Score:       0.30832255569348554

# Ciclo008 - Neural Network MLP

Neste ciclo faço no detalhe apenas a REde Neural, mantendo o mesmo resultado do ciclo anterior.

Accuracy:          0.36634087519436426
Balanced Accuracy: 0.36500792894874645
Kappa Score:       0.30832255569348554

# Ciclo009 - Aplicando PCA

Neste ciclo aplico a tecnica de PCA nos dados que é um processo de mudança de espaço que ocorre atraves da combinação linear entre os eixos originais, com o PCA podemos reduzir o espaço de dados para uma dimensionalidade menor e com isso realizar operações algebricas mais facilmente. Um dos problemas do PCA é que perdemos a explicatividade dos dados, isso para reportar ao time de negócio é importante.

Vamos a performance sem PCA e com PCA.

Sem PCA:

Accuracy:           0.3673563291340082
Balanced Accuracy:  0.367859512466673
Kappa Score:        0.3094952951924361

Com PCA:

Accuracy:           0.3566781962999397
Balanced Accuracy:  0.3595810612238049
Kappa Score:        0.29887947727417963

Com PCA + Cross Validation

Avg Balanced Accuracy: 0.36 +/- 0.0044
Avg Kappa Accuracy: 0.2983 +/- 0.0043



Neste ciclo podemos notar que realmente o modelo que estamos utilizando não é compativel com o nosso problema de negócio, para o proximo ciclo iremos treinar outros tipos de modelo procurando o que melhor irá performar com o fenomeno.


# Ciclo010 - Treino de novos modelos

Neste etapa iremos treinar varios modelos de forma simples e o que melhor performar iremos realizar o Fine Tuning e rodar o Cross Validation

# Ciclo011 - Transformando a performance do modelo em performance de negocio



