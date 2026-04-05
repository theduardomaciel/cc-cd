## 1. Visão Geral

### Por que Aprendizagem de Máquina?

- Análise humana de dados é cara, subjetiva e não escala para grandes volumes.
- Técnicas tradicionais (planilhas, bancos de dados) só respondem consultas simples.
- AM permite extrair **conhecimento** de grandes conjuntos de dados e responder perguntas complexas.

### Definição

> "Área de pesquisa que dá aos computadores a habilidade de aprender sem ser explicitamente programados." — Arthur Samuel, 1959

> "Técnicas capazes de melhorar seu desempenho em uma dada tarefa utilizando experiências prévias." — Mitchell, 1997

### Aplicações Clássicas

|Sistema|Tarefa|
|---|---|
|SPHINX (1989)|Reconhecimento de fala|
|ALVINN (1989)|Condução autônoma de veículos|
|Fayyad et al. (1995)|Classificação de objetos celestes|
|TD-GAMMON (1992)|Jogar gamão|

### Aplicações Modernas

- Análise de redes sociais
- Dados biológicos
- Detecção de fraudes
- Diagnóstico médico
- Biometria
- Recomendação de filmes/séries

---

## 2. Algoritmos de AM

### Viés Indutivo

Todo algoritmo de AM possui um **viés**: tendência a privilegiar certas hipóteses.

- **Viés de busca:** como as hipóteses são pesquisadas (ex: preferência por hipóteses simples).
- **Viés de linguagem:** define o espaço de hipóteses (ex: variáveis discretas).

### Tipos de Dados

- **Estruturados:** planilhas, tabelas atributo-valor — mais fáceis para AM.
- **Não estruturados:** textos, DNA, páginas web — geralmente convertidos antes.

### Tipos de Aprendizado

|Tipo|Característica|
|---|---|
|**Supervisionado**|Tarefa preditiva; fornece entrada + saída correta|
|**Não-supervisionado**|Tarefa descritiva; algoritmo aprende por conta própria|
|**Semi-supervisionado**|Apenas algumas instâncias têm rótulo|
|**Por reforço**|Aprendizado por tentativa e erro em espaço desconhecido|

---

## 3. Aprendizagem Supervisionada

### Regressão

- **Objetivo:** aprender uma função que mapeia um exemplo a um **valor real**.
- Caso especial: séries temporais.
- **Exemplos de uso:** valor de imóvel, lucro de empréstimo, tempo de internação.
- **Técnicas:** Árvores de Regressão, Redes Neurais, SVM, Regressão Linear.

### Classificação

- **Objetivo:** aprender uma função que associa um exemplo a uma **classe**.
- **Exemplos de uso:** diagnóstico médico, spam vs. ham, função de proteína.
- **Técnicas:** Árvores de Decisão, Conjuntos de Regras, Redes Neurais, SVM, K-NN, Regressão Logística, Redes Bayesianas.

---

## 4. Avaliação de Modelos

### Matriz de Confusão

Para classificação binária (classe Positiva P e Negativa N):

||Predito P|Predito N|
|---|---|---|
|**Real P**|TP (Verdadeiro Positivo)|FN (Falso Negativo)|
|**Real N**|FP (Falso Positivo)|TN (Verdadeiro Negativo)|

### Medidas de Avaliação

|Medida|Fórmula|O que mede|
|---|---|---|
|**Acurácia**|(TP+TN) / (P+N)|Proporção de acertos|
|**Taxa de Erro**|(FP+FN) / (P+N)|Proporção de erros|
|**Recall (Sensibilidade)**|TP / P|Cobertura dos positivos reais|
|**Especificidade**|TN / N|Cobertura dos negativos reais|
|**Precision**|TP / (TP+FP)|Qualidade das predições positivas|
|**F-beta Score**|(1+β²) × precision × recall / (β²×precision + recall)|Balanço entre precision e recall|

### Curva ROC

- Originada na engenharia elétrica (detecção de objetos inimigos).
- Representa o **trade-off** entre benefícios (TPR) e custos (FPR).
- **TPR** = TP/P; **FPR** = FP/N.
- **AUC (Area Under the Curve):** resume a curva em um único escalar — quanto maior, melhor.

**Como construir (classificadores probabilísticos):**

1. Ordenar instâncias por probabilidade prevista (decrescente).
2. Partir do ponto (0,0).
3. Para cada instância: se TP → mover para cima; se FP → mover para a direita.

---

## 5. Métodos de Estimação de Desempenho

> **Problema:** um único escalar pode ser pouco informativo (variabilidade, classes desbalanceadas, overfitting).

**Paradigma geral:** treinar e testar separadamente.

### Hold-out

- Particiona os dados em **2/3 treino / 1/3 teste** (ou 80/20, 75/25, 90/10).
- ✅ Bom para grandes datasets.
- ❌ Estimativa pessimista; conjunto de teste pode não ser representativo.

### Subamostragem Aleatória

- Variação do hold-out repetido **k vezes**.
- Estimativa final = média das k medidas.
- ✅ Estimativa mais confiável.
- ❌ Instâncias podem nunca ser testadas.

### K-Fold Cross-Validation

- Divide os dados em **k subconjuntos** mutuamente exclusivos.
- A cada rodada, 1 fold é teste e os demais são treino.
- Normalmente **k = 10**.
- ✅ Todas as instâncias são testadas.
- ❌ Alto custo computacional; inadequado para datasets pequenos.

### Leave-One-Out (LOO)

- Caso especial do k-fold com **k = N** (tamanho do dataset).
- Cada fold tem exatamente 1 instância.
- ✅ Útil para datasets pequenos; estimativa confiável e determinística.
- ❌ Muito alto custo computacional.

### Bootstrap

- **Reamostragem com reposição.**
- Naturalmente: ~63,21% dos dados no treino; ~36,79% nunca selecionados (conjunto de teste).
- Fórmula de estimativa com k repetições:

$$Acc(M) = \frac{1}{k} \sum_{i=1}^{k} \left[0{,}6321 \times Acc(M)_{teste(i)} + 0{,}3679 \times Acc(M)_{trein(i)}\right]$$

- ✅ Sem parâmetros; simples de aplicar.
- ❌ Excessivamente otimista; problemático com classes desbalanceadas.

---

## 6. Aprendizado Não-Supervisionado

### Motivação

- Em muitos problemas reais os dados **não são rotulados** (custo, tempo, indisponibilidade).
- Objetivo: extrair padrões e estruturas nos dados automaticamente.

### Processo (6 etapas)

1. **Seleção de atributos** — remover irrelevantes; manter os informativos.
2. **Medida de proximidade** — quantificar similaridade/dissimilaridade; **normalizar** os atributos!
3. **Critério de agrupamento** — função objetivo que define o que é um grupo.
4. **Algoritmo de agrupamento** — revela a estrutura nos dados.
5. **Validação dos resultados** — grupos não vazios, protótipos representativos, número adequado de grupos.
6. **Interpretação dos resultados** — análise com apoio de especialistas.

### Agrupamento Hierárquico

**Aglomerativo (bottom-up):**

1. Cada objeto é um grupo unitário.
2. Iterativamente, une os dois grupos mais próximos.

**Divisivo (top-down):**

1. Todos os objetos num único grupo.
2. Iterativamente, divide o grupo com maior distância interna.

**Critérios de linkage (distância entre grupos):**

|Linkage|Fórmula|
|---|---|
|Single|Mínima distância entre pares de objetos|
|Complete|Máxima distância entre pares de objetos|
|Average|Média de todas as distâncias entre pares|

**Dendrograma:** representação visual da hierarquia de agrupamentos.

### K-Means (Agrupamento Particional)

- Cada objeto pertence a **exatamente um grupo**.
- Principal algoritmo de agrupamento particional.

**Algoritmo:**

1. Escolhe aleatoriamente **k** protótipos iniciais.
2. **Atualiza grupos:** aloca cada objeto ao protótipo mais próximo.
3. **Atualiza protótipos:** recalcula como média dos objetos do grupo.
4. Repete até convergência (minimizar função objetivo J).

**Função objetivo:** $$J = \sum_{i=1}^{k} \sum_{j \in C_i} d(x_j, y_i)$$

Onde $d$ é a distância Euclidiana quadrada entre o objeto $x_j$ e o protótipo $y_i$.

---

## Tags

#machine-learning #ciencia-de-dados #classificacao #regressao #clustering #avaliacao-de-modelos #k-means #cross-validation #roc-curve #UFAL