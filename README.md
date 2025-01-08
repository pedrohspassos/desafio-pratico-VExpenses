
# **Desafio Prático - VExpenses**
![Blog-VExpenses](https://github.com/user-attachments/assets/2999509a-0a11-4f80-9600-37ce863e142d)

Este repositório foi criado com o objetivo de apresentar o trabalho desenvolvido no estudo de caso para a vaga de estágio na área de Ciência de Dados da empresa VExpenses, especializada em soluções de gerenciamento e automação de despesas corporativas.

## ***Introdução***

Este projeto tem como objetivo a criação de um modelo de classificação capaz de prever se um usuário, baseado em suas interações em um site imobiliário, comprará ou não uma casa. O modelo será treinado utilizando um conjunto de dados que contém informações demográficas e comportamentais dos usuários, como idade, renda, tempo de navegação no site, e interação com anúncios.

O desafio é usar essas variáveis para prever a decisão de compra, que é representada pela variável alvo "Compra". Com isso, o projeto busca fornecer insights sobre o comportamento dos usuários e como essas características influenciam a decisão de compra de um imóvel.

Ao longo deste repositório, apresentamos um passo a passo detalhado do processo de construção do modelo, desde a análise inicial dos dados até a avaliação do desempenho do modelo final. O objetivo é fornecer uma abordagem didática para quem deseja aprender sobre técnicas de aprendizado de máquina aplicadas a problemas reais de negócios.

## ***Descrição do Projeto***

Este projeto é um desafio prático desenvolvido como parte do processo seletivo para uma vaga de estágio em Ciência de Dados. O objetivo é construir um modelo de classificação para prever se um usuário de um site imobiliário comprará ou não uma casa, com base em suas características demográficas e comportamentais.

Os dados foram divididos em dois conjuntos:

- **Conjunto de Treinamento**
  - 140 registros
  - Aproximadamente 70% do total
  - Este conjunto será utilizado para treinar o modelo de aprendizado de máquina e realizar a validação inicial do desempenho.

- **Conjunto de Teste**
  - 60 registros
  - Aproximadamente 30% do total
  - Este conjunto será utilizado para avaliar a eficácia do modelo treinado.

O **conjunto de treinamento** contém dados sobre os usuários e se eles compraram ou não uma casa, informações que serão usadas para treinar o modelo de classificação.

O **conjunto de teste** será utilizado para testar o desempenho do modelo em dados não vistos. Para esse conjunto, as respostas (compra ou não compra) não estão fornecidas, e o modelo será responsável por prever esses resultados.

Este projeto visa demonstrar as habilidades de análise de dados, processamento de informações e construção de modelos preditivos, essenciais para o cargo de estágio em Ciência de Dados.

# **Etapas**

Muitos dos passos estão explicados diretamente no próprio Jupyter Notebook. Neste README, fornecerei apenas informações mais gerais sobre as etapas anteriores à **interpretação dos resultados**, pois darei um foco maior a essa parte aqui.

Ambos os documentos se complementam, portanto, algumas informações presentes nesse README podem não estar no Jupyter Notebook e vice-versa. Por isso, recomendo analisar cada etapa com base em ambos os textos para uma compreensão completa.



## ***0. Entendendo o Dataset***

Nesta primeira etapa, o objetivo é importar as bibliotecas necessárias, carregar o dataset e realizar uma análise preliminar para entender melhor os dados com os quais estamos lidando. Isso inclui visualizar as primeiras linhas, verificar os tipos de dados de cada coluna e entender a distribuição dos dados. Também foi realizado uma análise para identificar valores atípicos e valores ausentes.

Dentre as principais atividades realizadas, temos:

- **Importação de Bibliotecas**: Foi usado bibliotecas como Pandas para manipulação dos dados, Matplotlib e Seaborn para visualizações, e Scikit-learn para modelagem.
- **Carregamento e Visualização Inicial**: Foi carregado o dataset e visualizamos as primeiras linhas e tipos de dados de cada coluna.
- Análise Descritiva: Também foi verificado estatísticas básicas das variáveis numéricas e a distribuição da variável alvo ("Compra").
- Identificação de Problemas: E por fim, foi investigado a presença de valores ausentes e possíveis outliers, como valores negativos no "Tempo no Site (min)".

Essa etapa ajudou a entender melhor os dados e a preparar o terreno para uma análise exploratória mais acertiva.

## ***1. Análise Exploratória de Dados (AED)***

A Análise Exploratória de Dados tem como objetivo obter uma compreensão mais profunda dos dados, identificar problemas potenciais e gerar hipóteses sobre o comportamento das variáveis.

Dentre as principais atividades realizadas, temos:
- **Análise das Relações com a Coluna Alvo**: Foram gerados gráficos para analisar a distribuição de cada variável e como ela se relaciona com a variável alvo Compra.
- **Matriz de Correlação**: A correlação entre as variáveis numéricas foi analisada para verificar relações significativas entre elas.
- **Outros Gráficos**: Além disso, gráficos como o scatterplot foram gerados para visualizar melhor as relações entre as variáveis.

Além disso, para uma análise mais detalhada e visual, foi utilizada a biblioteca [**ydata-profiling**](https://github.com/ydataai/ydata-profiling). Essa ferramenta automatiza a análise exploratória, gerando relatórios completos que oferecem insights valiosos sobre o dataset, como distribuição das variáveis, correlações e possíveis problemas. 

## ***2. Pré-Processamento***

Após a análise exploratória, a etapa de pré-processamento é fundamental para garantir a qualidade dos dados antes de aplicar modelos de aprendizado de máquina. Durante este processo, abordamos três pontos principais.

### **2.1 Tratamento de valores nulos**

O tratamento de valores nulos é uma etapa crucial no pré-processamento de dados, pois valores ausentes podem impactar diretamente a performance e a precisão dos modelos de aprendizado de máquina.

Podem gerar problemas como:
- **Perda de Informação**
  - Uma vez que se os valores ausentes forem ignorados, o modelo pode ser treinado com dados incompletos, o que pode levar a resultados imprecisos ou enviesados.
- **Erro de Execução de Algoritmos**
  - Pois, muitos algoritmos de aprendizado de máquina não conseguem lidar com valores nulos e podem gerar erros durante o treinamento ou a previsão.
- **Impacto nas Métricas**
  - Em modelos de regressão ou classificação, a presença de valores nulos pode afetar a análise de erros, tornando as métricas de avaliação

Abaixo esta um gráfico mostrando alguns dos valores nulos achados no dataset analisado.

![valores_nulos](https://github.com/user-attachments/assets/d051b18c-0802-44d0-b9bc-974663fdd501)

Existem algumas abordagens para lidar com valores nulos.
- **Removendo os Dados Nulos**
O objetivo aqui é excluir os registros que contêm valores nulos.

Essa abordagem é adequada quando apenas alguns registros estão incompletos. No entanto, pode prejudicar a qualidade do modelo, pois, ao remover um registro, também perdemos informações valiosas de outras colunas associadas a ele.

- **Imputação de Valores (Média/Mediana/Moda)**
O objetivo é preencher os registros com valores nulos com alguns valores estimados com base nos dados disponíveis.

Para **variáveis numéricas**, é comum substituir os valores nulos pela média ou pela mediana, dependendo da distribuição dos dados.

A **substituição pela média** é uma boa opção quando os dados seguem uma distribuição normal ou simétrica e quando não há outliers que possam distorcer seu valor, pois a presença desses extremos pode comprometer a qualidade dos modelos de machine learning.

A **substituição pela mediana**, por outro lado, é preferível quando os dados possuem uma distribuição assimétrica ou desconhecida. Isso ocorre porque a médiana é mais robusta a outliers, impedindo que valores extremos distorçam o conjunto de dados, já que ela representa o valor central da amostra.

Para **variáveis categóricas**, é comum substituir os valores nulos pela moda, ou seja, pelo valor mais frequente na variável. Essa é uma abordagem rápida e eficiente na maioria dos casos.

- **Imputação com Algoritmos de Machine Learning**

Essa é uma abordagem mais robusta, na qual algoritmos de machine learning são utilizados para prever os valores ausentes com base em outras características do conjunto de dados. Para isso, existem técnicas como KNN ou a Regressão	Logística.

Na **imputação por KNN**, os valores ausentes são preenchidos com base nos valores dos vizinhos mais próximos, levando em consideração as características semelhantes entre as amostras.

Já na **imputação por Regressão Logística**, utiliza-se um modelo de regressão logística para prever os valores ausentes com base nas outras variáveis do conjunto de dados.

Essas técnicas podem ser utilizadas quando a quantidade de dados ausentes é significativamente grande e a imputação simples não é suficiente para preservar a qualidade do modelo.


### **2.2 Tratamento das Variáveis Categóricas**

A conversão de variáveis categóricas em formatos numéricos é uma outra etapa essencial no pré-processamento de dados, especialmente quando se trabalha com modelos de aprendizado de máquina.

Isso ocorre porque a maioria dos algoritmos de aprendizado de máquina exige entradas numéricas para realizar cálculos e determinar padrões. Como por exemplo, cálculos de distância, correlações entre outras métricas.

Portanto, o objetivo principal desse tratamento é aprimorar a eficiência dos modelos que serão desenvolvidos.

Devido à baixa complexidade do dataset e ao fato de estarmos lidando com variáveis categóricas que podem assumir apenas valores binários, optei por realizar a **codificação direta** dessas variáveis. Essa escolha se mostrou eficiente, pois, como as categorias envolvem apenas dois valores possíveis (como, "sim" ou "não", "0" ou "1"), a conversão para formato numérico pode ser feita diretamente, sem a necessidade de recorrer a técnicas mais complexas, como one-hot encoding.

**One-hot encoding** é uma técnica amplamente utilizada no tratamento de variáveis categóricas, especialmente quando um atributo pode assumir mais de dois valores possíveis. Essa abordagem consiste em criar uma nova coluna para cada categoria, onde um valor binário (0 ou 1) indica a presença ou ausência de cada categoria para uma observação específica.

Seu uso é fundamental nesses casos, pois evita que os modelos interpretem erroneamente a existência de uma ordem ou relação hierárquica entre os valores transformados, o que poderia distorcer os resultados.

### **2.3 Tratamento de Valores Inconsistentes**

Essa etapa, é fundamental no pré-processamento de dados, pois, assim como nos casos anteriores, valores errôneos ou que não fazem sentido podem comprometer a qualidade e a confiabilidade do modelo de aprendizado de máquina.

Entre os tipos mais comuns de inconsistências estão os valores negativos em variáveis onde esses valores não deveriam existir, como em idade, preço, quantidade de produtos vendidos, entre outros.

Normalmente, valores negativos nessas variáveis indicam erros de coleta, falhas de entrada ou dados corrompidos, e sua presença pode gerar resultados distorcidos durante o treinamento do modelo. Portanto, é crucial identificar e corrigir esses valores antes de alimentar o modelo.

Como abordagens para lidar com esses casos, podemos **substituir os valores inconsistentes** por valores válidos, como a média ou a mediana. Outra alternativa é optar pela **remoção dos registros** que contêm esses valores inconsistentes. Uma abordagem adicional, embora menos utilizada devido à complexidade em determinadas situações, é **consultar o provedor dos dados** para verificar se a inconsistência é, de fato, um erro ou não.

No caso desse projeto, foi observado a presença de valores negativos na coluna ***"Tempo no Site (min)"***, o que claramente não faz sentido, já que o tempo de navegação em um site não pode ser negativo.

A abordagem adotada foi substituir os valores negativos por valores nulos (NaN) e, em seguida, realizar a substituição desses valores nulos pela **mediana**. A escolha da mediana foi feita com base no que foi comentado anteriormente, já que ela é mais robusta a valores extremos e outliers, garantindo uma imputação mais confiável e representativa do tempo que um usuário fica no site, sem ser influenciada por possíveis distorções nos dados. 

Essa estratégia assegura que os dados sejam consistentes e apropriados para a modelagem, melhorando a qualidade do modelo de aprendizado de máquina.

Por exemplo, imagine que a coluna "Tempo no Site (min)" contenha um valor muito alto, como 1000 minutos, o que poderia ser um outlier.
- Nesse caso, a **média** seria influenciada por esse valor extremo, tornando-a maior em relação aos demais valores da coluna.
- Já a **mediana**, por outro lado, continuaria refletindo de maneira mais fiel o comportamento central dos dados, pois não é impactada pelos eventuais outliers.


## ***3. Construção do Modelo de Machine Learning***

Nesta etapa, o foco é construir e treinar o modelo de machine learning para resolver o problema proposto. Após o tratamento dos dados, incluindo a remoção e substituição de valores nulos, além da transformação das variáveis categóricas, o próximo passo é selecionar o modelo adequado para obter o melhor desempenho.

Para a construção do modelo de machine learning, adotei uma abordagem comparativa, utilizando diferentes algoritmos de classificação para avaliar qual oferece o melhor desempenho para o problema em questão.

Para isso, foram utilizados quatro modelos para a classificação: 
- **Regressão Logística**
- **Árvore de Decisão**
- **Random Forest**  
- **Rede Neural**

A escolha da rede neural foi feita para analisar os resultados utilizando um modelo de maior complexidade em comparação com os demais, a fim de verificar se há diferenças significativas nos resultados obtidos.

Dividi essa etapa em duas abordagens. Primeiro, realizaremos a previsão sem o uso do método de validação cruzada. Em seguida, aplicaremos o método de validação cruzada e compararemos os resultados obtidos em ambos os casos.

### **3.1 Previsão sem Validação Cruzada**
Nesta etapa, foram realizados os seguintes passos para gerar os modelos:

- **Separação das variáveis independentes e da variável alvo**: Organizando os dados para identificar as variáveis explicativas e a variável a ser prevista.
- **Divisão dos dados em treino e teste**: Os dados foram divididos em 70% para treinamento e 30% para teste. Embora não exista uma divisão fixa, essa é a proporção mais comum utilizada.
- **Treinamento dos quatro modelos selecionados**: Os modelos foram treinados com base no conjunto de dados de treinamento.
- **Avaliação da performance dos modelos**: A performance dos modelos foi avaliada utilizando o conjunto de teste, a fim de verificar como eles se comportam com dados novos
- **Exibição dos relatórios de classificação**: Foram gerados relatórios contendo as métricas de avaliação, como precisão, recall, F1-score e acurácia, para uma análise detalhada do desempenho de cada modelo.

Após a conclusão desses passos, foi gerado um gráfico exibindo os resultados de acurácia obtidos pelos modelos, como pode ser observado a seguir.

![resultados_sem_cv](https://github.com/user-attachments/assets/6273ae19-445d-492f-8efe-3eb789bda7d9)


Podemos ver que o modelo que apresentou o ***melhor desempenho*** foi a **Árvore de Decisão**, que obteve a maior acurácia entre todos os modelos testados. Isso sugere que a simplicidade e a capacidade de interpretação dessa técnica foram vantajosas para este conjunto de dados, permitindo que ela capturasse de forma eficaz as relações entre as variáveis.

Os modelos que apresentaram os ***piores desempenhos*** foram o **Random Forest** e a **Rede Neural (MLP)**. Ambos ficaram atrás da Árvore de Decisão em termos de acurácia. Isso pode indicar que, neste caso específico, esses modelos mais complexos não se ajustaram tão bem aos dados ou que a configuração dos parâmetros pode não ter sido a mais adequada, o que comprometeu sua capacidade de generalização para o conjunto de teste.

### **3.2 Previsão com Validação Cruzada**

A validação cruzada é uma técnica utilizada em aprendizado de máquina para avaliar a performance de um modelo de forma mais robusta. Ela tem como objetivo reduzir a variação nos resultados e garantir que o modelo não esteja superajustado (overfitted) aos dados de treinamento.

O termo **underfitting**, é usado quando um modelo é muito simples para capturar os padrões e relações presentes nos dados. Isso acontece geralmente quando o modelo não possui complexidade suficiente para aprender as características subjacentes dos dados, o que leva a um desempenho fraco tanto no conjunto de treinamento quanto no conjunto de teste.

Já o termo **overfitting**, é usado quando o modelo "aprende demais" os detalhes dados de treinamento, capturando até padrões irrelevantes ou específicos demais para esse conjunto de dados. Essa características, que a princípio parece ser positiva, faz com que o modelo tenha um desempenho muito bom no conjunto de treinamento, mas se saia mal no conjunto de teste, isso é, o modelo se adapta excessivamente aos dados de treinamento, tornando-se muito específico e, portanto, menos eficaz quando exposto a dados desconhecidos.

Logo, a validação cruzada é uma das técnicas usadas pare resolver esse problema.

#### **3.2.1 Funcionamento da Validação Cruzada***

Na validação cruzada, o conjunto de dados é dividido em múltiplos subconjuntos, os chamados ***folds***.

O conjunto de dados é dividido em **k folds** de tamanho aproximadamente igual, para cada uma das k iterações, o modelo é treinado em **k-1 folds** e testado no fold restante. Isso é, ele é treinado k vezes, utilizando um fold diferente como conjunto de teste a cada vez

O desempenho do modelo é avaliado em cada iteração, e ao final, as métricas de desempenho são **média das avaliações** de todas as iterações.

Essa abordagem é extremamente interessante, pois nos permite ter um maior controle sobre eventuais distorções que poderiam ocorrer devido a uma única divisão de dados entre treino e teste. Ao realizar a validação cruzada, temos várias divisões dos dados, o que reduz significativamente o risco de uma divisão específica, que poderia beneficiar ou prejudicar o modelo, tornando-o enviesado.

Com mais separações dos dados, garantimos que o modelo seja avaliado em diferentes contextos e condições, o que ajuda a obter uma medida mais confiável e generalizável de seu desempenho. Isso torna a avaliação do modelo mais robusta, pois evitamos que o desempenho do modelo seja afetado por uma divisão particular que poderia não ser representativa do comportamento real dos dados.

Esse tipo de validação cruzada tem o nome de ***k-fold cross-validation***.

#### **3.2.2 Etapas**

As etapas seguem basicamente a mesma estrutura da etapa anterior, com algumas mudanças pontuais. Entretanto, etapas como a separação das variáveis e a divisão entre treino e teste não são realizadas de maneira explícita, como na etapa anterior. 

Isso ocorre porque podemos reutilizar a separação das variáveis, e, ao tratar-se de validação cruzada, a própria função ***cross_val_score()*** será responsável por dividir os dados em treino e teste automaticamente, além de calcular e retornar a acurácia média durante o processo de validação cruzada.

Após a conclusão desses passos, foi gerado um gráfico exibindo os resultados de acurácia obtidos pelos modelos, como pode ser observado a seguir.

![resultado_com_cv](https://github.com/user-attachments/assets/6e7ae7f3-37ec-402d-854b-eca90046c75b)

Podemos obervar que o modelo que apresentou o **melhor desempenho** nesse novo contexto foi a **Rede Neural (MLP)**, obtendo a maior acurácia entre os demais. 

Já o modelo que apresentou o **pior desempenho** foi a **Árvore de Decisão**, obtendo a pior acurácia.

### **3.3 Comparação**

Uma vez realizada ambas abordagens, vamos analisar um pouco as diferenças obtidas.

![comparacao](https://github.com/user-attachments/assets/3f15f254-2439-4cc1-beb5-82114a468592)

Uma observação interessante é que os papéis dos modelos se inverteram ao utilizarmos a validação cruzada na construção dos modelos. 

Enquanto, ***sem a validação cruzada***, o melhor modelo era a **Árvore de Decisão** e o pior modelo era a **Rede Neural**, com a introdução da ***validação cruzada***, a **Árvore de Decisão** passou a ter o pior desempenho, enquanto a **Rede Neural** se destacou como o melhor modelo.

Esse fenômeno pode ser explicado pelo fato de que a validação cruzada oferece uma avaliação mais robusta e generalizada do desempenho dos modelos. Ela permite que o modelo seja testado em diferentes divisões dos dados, reduzindo o risco de sobreajuste (overfitting) e proporcionando uma avaliação mais fiel à sua capacidade de generalização

Assim, enquanto a **Árvore de Decisão** pode ter se beneficiado de uma divisão específica dos dados, a **Rede Neural**, com sua capacidade de capturar padrões mais complexos, teve seu potencial melhor aproveitado e mostrou-se mais eficaz com a validação cruzada.

Logo, podemos dizer que no caso dos modelos sem validação
cruzada a **Árvore de Decisão** pode ter se saído melhor porque se ajustou bem aos dados de treino específicos, sem a preocupação de generalizar em diferentes conjuntos de dados. Isso pode ter dado uma falsa sensação de bom desempenho.

Já com a validação cruzada, a **Rede Neural** mostrou sua capacidade de generalização, uma vez que foi exigida uma avaliação mais rigorosa e robusta do desempenho do modelo.


## ***4. Ajustando Hiperparâmetros***

## 🛠 Ferramentas
- Python 
- Bibliotecas 
    - Pandas
    - NumPy
    - YData Profiling
    - Scikit Learn 
    - Seaborn
    - Matplotlib
## Referências

- [Pandas](https://pandas.pydata.org/)
- [NumPy](https://numpy.org/)
- [YData Profiling](https://github.com/ydataai/ydata-profiling)
- [Scikit Learn](https://scikit-learn.org/stable/index.html)
- [Seaborn](https://seaborn.pydata.org/)
- [Matplotlib](https://matplotlib.org/)


## Autor

- [@pedrohspassos](https://github.com/pedrohspassos)

