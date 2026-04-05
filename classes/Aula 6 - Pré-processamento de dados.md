## Por que pré-processar?

No mundo real, os dados estão sujeitos a **ruídos**, **outliers**, **elementos faltantes** e **inconsistências**. Baixa qualidade dos dados leva a baixa qualidade na mineração.

O objetivo é melhorar: acurácia, abrangência, consistência, confiabilidade e interpretabilidade.

**Etapas da mineração de dados:** Dados → Seleção → Pré-processamento → Transformação → Mineração → Conhecimento

---

## Tarefas principais

### 1. Limpeza de dados

**Dados faltantes — 6 abordagens:**

1. Ignorar a tupla
2. Preencher manualmente
3. Preencher com valor global (ex: "NaN", −∞)
4. Preencher com estatísticas (média ou mediana)
5. Preencher com estatísticas por classe
6. Preencher com valor mais provável (regressão, árvore de decisão, inferência)

**Dados ruidosos — 3 abordagens:**

1. **Binning:** ordena os dados, divide em bins de igual frequência e suaviza pela média ou pela fronteira do bin
2. **Regressão:** ajusta uma curva aos dados para identificar e corrigir pontos fora do padrão
3. **Análise de outliers:** detecta pontos que ficam fora dos clusters principais

---

### 2. Integração de dados

Objetivo: combinar múltiplas fontes com semântica heterogênea, reduzindo redundância e inconsistência.

1. **Identificação de entidade:** garantir que campos de fontes diferentes representam o mesmo conceito — solução: uso de metadados
2. **Análise de redundância e correlação:**
    - χ²-quadrado para atributos nominais
    - Coeficiente de correlação (−1 a 1) para atributos numéricos
    - Covariância para atributos numéricos
3. **Duplicação de tuplas:** identificar e remover registros idênticos causados por atualizações parciais
4. **Conflito de valores:** padronizar notação e semântica (ex: pesos em métricas diferentes, moedas, escalas de notas)

---

### 3. Redução de dados

Conjuntos muito grandes podem tornar a mineração lenta, prejudicar modelos de aprendizado de máquina e dificultar a interpretação.

**Redução de dimensionalidade** (reduz o número de variáveis):

- **Wavelet transform:** calcula coeficientes wavelet e gera um conjunto esparso
- **PCA (Principal Components Analysis):** calcula vetores ortogonais e projeta os dados nos mais relevantes
- **Seleção de subconjuntos de atributos:** usa heurísticas forward/backward

**Redução de numerosidade** (reduz o número de tuplas):

- **Histograma:** agrega tuplas em bins, conservando as características dos dados
- **Agrupamento:** divide os dados em grupos; protótipos substituem os dados originais
- **Amostragem:** seleção aleatória sem reposição, com reposição ou estratificada

---

### 4. Transformação de dados

Objetivo: consolidar os dados em uma forma que permita processamento mais rápido e eficaz.

|Abordagem|Descrição|
|---|---|
|Smoothing|Remove variações bruscas nos dados|
|Construção de atributos|Combina features existentes para criar novas (ex: F₃ = F₁ × F₂)|
|Agregação|Resume dados por dimensões (ex: por ano, marca, cor)|
|Normalização|Coloca variáveis em mesma escala (ex: padronização z-score)|
|Discretização|Converte valores contínuos em categorias ou intervalos|
|Geração de hierarquia|Organiza dados em níveis (Cidade → Estado → País → Todos)|

---

## Exemplo em Python (scikit-learn)

```python
import numpy as np
import pandas as pd
from sklearn.impute import SimpleImputer
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, LabelEncoder, OneHotEncoder

# 1. Importar dados
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[:, :-1].values  # atributos independentes
Y = dataset.iloc[:, -1].values   # variável dependente

# 2. Tratar valores faltantes (substitui NaN pela média)
imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
X[:, 1:] = imputer.fit_transform(X[:, 1:])

# 3. Codificar dados categóricos
X[:, 0] = LabelEncoder().fit_transform(X[:, 0])
X = OneHotEncoder(categorical_features=[0]).fit_transform(X).toarray()
Y = LabelEncoder().fit_transform(Y)

# 4. Dividir em treino e teste
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=0)

# 5. Normalizar as variáveis
sc = StandardScaler()
X_train = sc.fit_transform(X_train)
X_test  = sc.transform(X_test)
```

---

## Referências

- Han, Pei & Kamber (2011). _Data Mining: Concepts and Techniques_. Elsevier.
- https://towardsdatascience.com/data-preprocessing-in-python-b52b652e37d5