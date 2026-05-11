# Ciência de Dados — Regressão

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Regressão Simples
- Regressão Múltipla
- Regressão Logística
- Aplicação

---

# Análise de Regressão

A análise de regressão estuda a relação entre variáveis:

- Variável dependente;
- Variáveis independentes.

O relacionamento é representado por um modelo matemático.

---

# Aplicações

- Seleção de variáveis;
- Análise de outliers;
- Interpretação de comportamento;
- Previsão de observações futuras.

---

# Dados

Os dados possuem a forma:

$$
(x_1,y_1),(x_2,y_2),\dots,(x_n,y_n)
$$

---

# Regressão Linear Simples

## Modelo

$$
Y = E(Y|X=x)+\varepsilon
=
\alpha+\beta x+\varepsilon
$$

Onde:

- $Y$: variável dependente;
- $X$: variável independente;
- $\alpha$: intercepto;
- $\beta$: inclinação;
- $\varepsilon$: erro aleatório.

---

## Modelo para $n$ observações

$$
Y_i=\alpha+\beta x_i+\varepsilon_i
$$

Assume-se:

$$
E(\varepsilon_i)=0
$$

$$
Var(\varepsilon_i)=\sigma^2
$$

---

# Método dos Mínimos Quadrados (MMQ)

Deseja minimizar:

$$
SQ(\alpha,\beta)=
\sum_{i=1}^{n}
(y_i-\alpha-\beta x_i)^2
$$

---

## Estimadores

$$
\hat{\alpha}= \bar{y}-\hat{\beta}\bar{x}
$$

$$
\hat{\beta}=
\frac{
\sum x_i y_i - n\bar{x}\bar{y}
}{
\sum x_i^2 - n\bar{x}^2
}
$$

---

## Reta estimada

$$
\hat{y}=\hat{\alpha}+\hat{\beta}x
$$

---

# Resíduo

$$
e_i=y_i-\hat{y}_i
$$

Resíduos pequenos indicam:

- Bom ajuste;
- Modelo representativo.

---

# Regressão Linear Múltipla

## Objetivo

Entender o comportamento da variável dependente a partir de várias variáveis independentes.

---

## Modelo

$$
y_i=
\beta_0+\beta_1x_{1i}+\beta_2x_{2i}+\dots+\beta_kx_{ki}+\varepsilon_i
$$

---

# Abordagem Matricial

$$
y=X\beta+\varepsilon
$$

---

# Estimação MMQ

$$
\hat{\beta}=
(X'X)^{-1}X'y
$$

Condição:

- $X'X$ deve ser não singular.

---

# Regressão Logística

## Objetivo

Predizer variáveis categóricas:

- Bom ou mau pagador;
- Solvente ou insolvente.

---

## Características

- Variável dependente binária;
- Variáveis independentes podem ser categóricas ou numéricas.

---

# Probabilidade

$$
P(Y_i=1)=\pi_i
$$

$$
P(Y_i=0)=1-\pi_i
$$

---

# Logit

$$
logit(p)=
\ln\left(
\frac{p}{1-p}
\right)
$$

---

# Função logística

$$
p=
\frac{e^x}{1+e^x}
$$

---

# Modelo Logístico

$$
E(Y)=
\frac{
exp(\beta_0+\beta_1X)
}{
1+exp(\beta_0+\beta_1X)
}
$$

---

# Aplicação

## Exemplo

Variáveis:

- Tempo de CPU;
- Número de I/Os;
- Memória utilizada.

Modelo:

$$
CPU=
b_0+b_1(IO)+b_2(mem)
$$

Resultado:

$$
b=
[-0.1614,\ 0.1182,\ 0.0276]
$$

---

## Equação Final

$$
CPU=
-0.1614
+
0.1182(IO)
+
0.0276(mem)
$$

---

## Coeficiente de determinação

$$
R^2=0.97
$$

---

# Referências

- https://www.ime.usp.br/~fmachado/MAE229/AULA10.pdf
- http://hedibert.org/wp-content/uploads/2014/02/Econometria201401-Aula04-ARLM-I-Estimacao.pdf
- https://homepages.dcc.ufmg.br/~jussara/metq/aula6-2017-1-parte2.pdf
- https://edisciplinas.usp.br/pluginfile.php/3769787/mod_resource/content/1/09_RegressaoLogistica.pdf

---

# Próxima Aula

Árvore de Decisão