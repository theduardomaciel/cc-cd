### O que é Estatística?

Ciência dedicada à **coleta, análise e interpretação de dados**, originada da expressão latina _statisticum collegium_ (assuntos de Estado). Abrange métodos de coleta, organização, resumo, apresentação e conclusão sobre dados.

**Ramos principais:**

- **Estatística Descritiva** — descreve e sumariza conjuntos de dados
- **Probabilidade** — quantifica a incerteza de eventos
- **Hipótese e Inferência** — avalia suposições sobre os dados

---

### Estatística Descritiva

**Técnicas de Visualização** (dependem do tipo de dado — qualitativo ou quantitativo):

- Gráfico de Barras, Pizza, Histograma, Linha e Dispersão
- Implementados em Python com `matplotlib` e `sklearn`

**Medidas de Tendência Central:** Média, Mediana, Moda

**Medidas de Variabilidade:** Amplitude, Variância, Desvio-padrão, Coeficiente de variação

**Quartis** — dividem os dados em 4 partes iguais:

- Q1 = 25%, Q2 = 50% (mediana), Q3 = 75%

**Boxplot** — representa a variação dos dados via quartis, destacando outliers (valores fora de Q1 − 1,5·IQR e Q3 + 1,5·IQR)

---

### Probabilidade

- P(E) = nº de possibilidades de E / total de possibilidades
- **Eventos independentes:** P(E,F) = P(E)·P(F)
- **Eventos dependentes:** P(E,F) = P(E|F)·P(F)
- **Teorema de Bayes** — "reverte" probabilidades condicionais:
    - Exemplo clássico: P(doença) = 0,01%, P(teste|doença) = 99% → P(doença|teste) ≈ 0,98%

**Distribuições:**

- _Discreta_: resultados contáveis (ex: cara/coroa)
- _Contínua_: resultados contínuos (ex: horas)
- **Distribuição Normal** — a "rainha das distribuições", formato de sino, definida pela média (µ) e variância (σ²)

---

### Hipótese e Inferência

**Teste de Hipótese** — decide entre H₀ (nula) e H₁ (alternativa) com base em estatísticas, assumindo um nível de significância α.

|Decisão|H₀ verdadeira|H₁ verdadeira|
|---|---|---|
|Aceitar H₀|✅ Decisão certa|❌ Erro Tipo II|
|Rejeitar H₀|❌ Erro Tipo I|✅ Decisão certa|

**Tipos de teste** (conforme dados e número de amostras):

- T-Test (1 ou 2 amostras), ANOVA (>2 amostras), Chi-Square, F-Test, Wilcoxon, Mann-Whitney, Kruskal-Wallis

**P-value** — probabilidade de obter uma estatística tão extrema quanto a observada. P-value < α → rejeita H₀.

**Teste de Normalidade (Shapiro-Wilk)** — verifica se a amostra segue distribuição normal; visualizado via histograma e QQ-plot.

**Intervalo de Confiança** — estimativa por intervalo de um parâmetro populacional, com nível de confiança (1 − α), útil para comparar grupos visualmente.

---

### Ferramentas Python utilizadas

`numpy`, `matplotlib`, `scipy.stats`, `statistics`, `statsmodels`, `sklearn`