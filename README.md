# Criação de um modelo de Machine Learning para prever ataques de phishing utilizando Python
#### Autor: Guilherme Oliveira da Rocha Cunha

## Coleta de dados
O conjunto de dados utilizado foi o [**Phishing Dataset for Machine Learning**](https://www.kaggle.com/datasets/shashwatwork/phishing-dataset-for-machine-learning) disponibilizado no Kaggle pelo seu proprietário Shashwat Tiwari e possui licença Attribution 4.0 International (CC BY 4.0). O conjunto de dados contém aproximadamente 1,34 MB, disposto em 1 planilha do tipo csv nomeada "Phishing_Legitimate_full".

Conforme sua descrição no Kaggle, este conjunto de dados contém 48 atributos (features) extraídos de 5.000 webpages de phishing e de 5.000 webpages legítimas, que foram baixadas de janeiro a maio de 2015 e de maio a junho de 2017.

## Preparação dos dados
Foi verificado o seguinte: 
- Todos os atributos do dataset são do tipo numérico, não houve necessidade de utilizar técnincas como get dummies ou one-hot-encoding.
- Esse dataset não possui valores nulos.
- A variável alvo (target) é definida pelo atributo 'CLASS_LABEL', que assume valor 1 em caso de phishing e 0 caso contrário. Portanto, a métrica de avaliação se dá por classificação.
- O dataset está bastante balanceado: 50% das observações do tipo phishing e 50% do tipo legítimo.

Serão utilizados e comparados dois algoritmos: **Random Forest** e **Decision Tree**.

### Algoritmo Random Forest






