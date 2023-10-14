# Criação de um modelo de Machine Learning para prever ataques de phishing utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

### Coleta de dados
O conjunto de dados utilizado foi o [**Phishing Dataset for Machine Learning**](https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning) disponibilizado no Kaggle pelo seu proprietário Shashwat Tiwari e possui licença Attribution 4.0 International (CC BY 4.0). O conjunto de dados contém aproximadamente 1,34 MB, disposto em 1 planilha do tipo csv nomeada "Phishing_Legitimate_full".

Conforme sua descrição no Kaggle, este conjunto de dados contém 48 features (atributos) extraídos de 5.000 webpages de phishing e de 5.000 webpages legítimas, que foram baixadas de janeiro a maio de 2015 e de maio a junho de 2017.

### Preparação dos dados
Foi verificado o seguinte: 
- Todos os atributos do dataset são do tipo numérico, não houve necessidade de utilizar técnincas como get dummies ou one-hot-encoding.
- Esse dataset não possui valores nulos ou erros, não será necessária a etapa de limpeza dos dados.
- A classe target (variável alvo) é definida pelo atributo 'CLASS_LABEL', que assume valor 1 em caso de phishing e 0 caso contrário. Portanto, a métrica de avaliação se dá por classificação.
- O dataset está bastante balanceado: 50% das observações do tipo phishing e 50% do tipo legítimo.

Serão utilizados e comparados dois algoritmos: **Random Forest** e **Decision Tree**.

## Algoritmo Random Forest
Foram realizadas as seguintes etapas:
1. Inicialmente foi gerada uma matriz de correlação para verificar a correlação das features com a classe target. Após a visualização de matriz de correlação, foi feito o drop (remoção) das features importantes como 'id' (index) e target('CLASS_LABEL'), que caso ficassem ocasionaria um overfitting (sobreajuste) do treino. A feature 'HttpsInHostname' também sofreu drop por não ter correlação com os dados, já que tem o mesmo valor de campo em todas as linhas (todas as observações estão com valor 0).
2. Para a divisão dos dados foi feita a divisão de 80% pra treino e 20% pra teste.
3. Foi feito o Feature Scaling com objetivo de padronizar os dados utilizando o método StandardScaler.





