# Criação de um modelo de Machine Learning para prever ataques de phishing utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

## 1. Coleta de dados
O conjunto de dados utilizado foi o [**Phishing Dataset for Machine Learning**](https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning) disponibilizado no Kaggle pelo seu proprietário Shashwat Tiwari e possui licença Attribution 4.0 International (CC BY 4.0). O conjunto de dados contém aproximadamente 1,34 MB, disposto em 1 planilha do tipo csv nomeada "Phishing_Legitimate_full".

Conforme sua descrição no Kaggle, este conjunto de dados contém 48 features (atributos) extraídos de 5.000 webpages de phishing e de 5.000 webpages legítimas, que foram baixadas de janeiro a maio de 2015 e de maio a junho de 2017.

## 2. Preparação dos dados
Foi verificado o seguinte: 
- Todas as features do dataset são do tipo numérico, não houve necessidade de utilizar técnicas como get dummies ou one-hot-encoding.
- Esse dataset não possui valores nulos ou erros, não foi necessária a etapa de limpeza dos dados.
- A classe target (variável alvo) é definida pela feature CLASS_LABEL, que assume valor 1 em caso de phishing e 0 caso contrário.
- Como o objetivo é identificar se é phishing ou não, a métrica de avaliação se dará por classificação.
- O dataset está bastante balanceado: 50% das observações do tipo phishing e 50% do tipo legítimo.

### 2.1. Feature selection
Foi selecionado o método SelectKBest que seleciona as melhores "K" características com base em uma métrica específica, que nesse caso foi escolhida a função f_classif que é adequada quando os dados são numéricos e a variável alvo é categórica. Foram usadas um total de 30 features.
Não foi utilizada a matriz de correlação pois em casos onde há um relacionamento não-linear, a matriz geralmente não é uma boa medida.

### 2.2. Divisão dos dados
Foi definido 80% para treinamento e 20% para teste.

## 3. Escolha do algoritmo e Treinamento do modelo
Para esse problema de classificação foi escolhido o Random Forest. Não foi necessário aplicar um método de padronização (normalização/escalonamento) aos atributos. A maioria dos algoritmos baseados em árvores são invariantes à escala das features, o que significa que a mudança na escala das features não afeta seu desempenho. 

## 4. Avaliação do desempenho
Foram utilizadas as seguintes métricas de avaliação de desempenho:
- Precision: Número de exemplos classificados como pertencentes a uma classe, que realmente são daquela classe (positivos verdadeiros), dividido pela soma entre este número, e o número de exemplos classificados nesta classe, mas que pertencem a outras (falsos positivos).
- Recall: Número de exemplos classificados como pertencentes a uma classe, que realmente são daquela classe, dividido pela quantidade total de exemplos que pertencem a esta classe, mesmo que sejam classificados em outra. No caso binário, positivos verdadeiros divididos por total de positivos.
- F1-Score: é uma média harmônica entre precisão e recall.
- Accuracy: É o número de acertos (positivos) divido pelo número total de exemplos.
- Support: O support não é uma métrica de desempenho, mas sim uma contagem das instâncias de cada classe no conjunto de dados.

Referência: FILHO, Mario. **As Métricas Mais Populares para Avaliar Modelos de Machine Learning**. 2018. Disponível em: https://mariofilho.com/as-metricas-mais-populares-para-avaliar-modelos-de-machine-learning/

## 5. Learning Curve
Foi gerada uma learning curve para detectar overfitting ou underfitting e avaliar a necessidade de mais dados.

## Resultados
### Métricas de avaliação
![RF_result](https://github.com/Gui-lherme-Oliv/PhishingPrediction_ML/assets/123426025/ed8f3821-f604-49f6-9a9a-41bcf00116a5)

A partir desses valores pode-se chegar às seguintes conclusões:
-  Precision: Um valor de 0.98 indica que o modelo raramente faz falsos positivos, ou seja, quando ele prevê uma classe como positiva, é altamente provável que seja realmente positiva.
-  Recall: Um valor de 0.98 indica que o modelo captura quase todos os exemplos positivos e tem um desempenho excelente em identificar a classe positiva.
-  F1-Score: Um valor de 0.98 indica um ótimo equilíbrio entre precisão e revocação.
-  Accuracy: Um valor de 0.98 indica que o modelo é altamente preciso em sua classificação global.

Com esses resultados satisfatórios não será necessário realizar o ajuste de hiperparâmetros nem de testar algum outro algoritmo de machine learning.

### Learning Curve
![RF_lc](https://github.com/Gui-lherme-Oliv/PhishingPrediction_ML/assets/123426025/ac062ffb-b9ec-43be-abc2-3485e20aaf73)

A partir do gráfico pode-se observar que o training score permanece alto independentemente do tamanho do conjunto de treinamento. Por outro lado, o cross-validation score aumenta com o tamanho do conjunto de dados de treinamento. Na verdade, aumenta até um ponto em que atinge um patamar. Observar tal patamar é uma indicação de que pode não ser útil adquirir novos dados para treinar o modelo, uma vez que o desempenho do modelo não aumentará mais
