# Criação de um modelo de Machine Learning para prever ataques de phishing utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

### Coleta de dados
O conjunto de dados utilizado foi o [**Phishing Dataset for Machine Learning**](https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning) disponibilizado no Kaggle pelo seu proprietário Shashwat Tiwari e possui licença Attribution 4.0 International (CC BY 4.0). O conjunto de dados contém aproximadamente 1,34 MB, disposto em 1 planilha do tipo csv nomeada "Phishing_Legitimate_full".

Conforme sua descrição no Kaggle, este conjunto de dados contém 48 features (atributos) extraídos de 5.000 webpages de phishing e de 5.000 webpages legítimas, que foram baixadas de janeiro a maio de 2015 e de maio a junho de 2017.

### Preparação dos dados
Foi verificado o seguinte: 
- Todas as features do dataset são do tipo numérico, não houve necessidade de utilizar técnicas como get dummies ou one-hot-encoding.
- Esse dataset não possui valores nulos ou erros, não será necessária a etapa de limpeza dos dados.
- A classe target (variável alvo) é definida pela feature CLASS_LABEL, que assume valor 1 em caso de phishing e 0 caso contrário.
- Como o objetivo é identificar se é phishing ou não, a métrica de avaliação se dará por classificação.
- O dataset está bastante balanceado: 50% das observações do tipo phishing e 50% do tipo legítimo.

Foram utilizados e comparados dois algoritmos: **Random Forest** e **Decision Tree**. Para ambos os modelos gerados foram utilizadas as seguintes métricas de avaliação de desempenho:
- Precision: Número de exemplos classificados como pertencentes a uma classe, que realmente são daquela classe (positivos verdadeiros), dividido pela soma entre este número, e o número de exemplos classificados nesta classe, mas que pertencem a outras (falsos positivos).
- Recall: Número de exemplos classificados como pertencentes a uma classe, que realmente são daquela classe, dividido pela quantidade total de exemplos que pertencem a esta classe, mesmo que sejam classificados em outra. No caso binário, positivos verdadeiros divididos por total de positivos.
- F1-Score: é uma média harmônica entre precisão e recall.
- Accuracy: É o número de acertos (positivos) divido pelo número total de exemplos.
- Support: O support não é uma métrica de desempenho, mas sim uma contagem das instâncias de cada classe no conjunto de dados.

Referência: FILHO, Mario. **As Métricas Mais Populares para Avaliar Modelos de Machine Learning**. 2018. Disponível em: https://mariofilho.com/as-metricas-mais-populares-para-avaliar-modelos-de-machine-learning/

## Algoritmo Random Forest
Foram realizadas as seguintes etapas:
1. **Matriz de correlação:** Inicialmente foi gerada uma matriz de correlação para verificar a correlação das features com a classe target.
2. **Feature Selection:** Após a visualização de matriz de correlação, foi feito o drop (remoção) das features importantes como id (index) e CLASS_LABEL (target), que caso ficassem ocasionaria um overfitting (sobreajuste) do treino. A feature HttpsInHostname também sofreu drop por não ter correlação com os dados, já que tem o mesmo valor de campo em todas as linhas (todas as observações estão com valor 0).
3. **Divisão dos dados:** foi feita a divisão dos dados em 80% para treino e 20% para teste.
4. **Feature Scaling:** realizado com objetivo de padronizar os dados utilizando o método StandardScaler.
5. **Treinamento do modelo**.
6. **Avaliação do desempenho** 
### Resultados
![RF](https://github.com/Gui-lherme-Oliv/PhishingPrediction_ML/assets/123426025/8abfbf47-d49b-4d50-a67e-16b70a35eebf)

## Algoritmo Decision Tree
Foram realizadas as seguintes etapas:
1. **Matriz de correlação:** Inicialmente foi gerada uma matriz de correlação para verificar a correlação das features com a classe target.
2. **Feature Selection:** Através da análise da matriz de correlação, foram removidas as features id, HttpsInHostname e CLASS_LABEL, pelos mesmos motivos apresentados na etapa do Random Forest. Além disso, como o modelo será feito por Decision Tree, a Feature Selection será feita utilizando os valores da matriz de correlação. Portanto, a partir da correlação entre a CLASS_LABEL (target) e todas as outras features, foram removidas as features com a correlação mais fraca com o target.
3. **Divisão dos dados:** foi feita a divisão dos dados em 80% para treino e 20% para teste.
4. **Treinamento do modelo**.
5. **Plotagem da Decision Tree**: A Árvore de Decisão foi plotada com uma profundidade máxima igual a 3.
6. **Learning Curve:** Feito todo o processo de criação da Learning Curve para para verificar se há ou não overfitting do treinamento do modelo, inclusive a ordenação dos índices do dataset, afim de verificar de forma decrescente as features mais importantes para o treino. Para a função da Learning Curve foi utilizado o f1_score por motivo da Decision Tree ser de classificação. Dessa forma, foi acompanhado todo o processo do f1_score a partir do aumento de uso de features no treinamento e no teste, a fim de verificar se há ou não overfitting do modelo. Por fim foi verificado que não existe overfitting no modelo.

  
7. **Avaliação do desempenho**

### Resultados







Uso do Learning Curve/ Analise under/overfiting: verificada o learning curve a partir do f1_score, não foi verificado overfitting no teste.
