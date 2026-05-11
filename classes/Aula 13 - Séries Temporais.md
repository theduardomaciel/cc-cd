# Ciência de Dados - Séries Temporais

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Introdução
- Fenômenos Típicos
- Modelos de Séries Temporais
- Análise de Séries Temporais

---

# Introdução

## Série Temporal (Time Series — TS)

- Sequência de números;
- Coletados em intervalos regulares;
- Durante um período de tempo;
- Tempo discreto;
- Observações vizinhas dependentes.

## Estudos de Séries Temporais

### Modelagens

- Análise da dependência;
- Técnicas específicas a séries temporais.

### Exemplos de aplicações

- Economia: preços diários de ações; taxa de desemprego;
- Medicina: níveis de eletrocardiograma ou eletroencefalograma;
- Epidemiologia: casos semanais de sarampo; casos mensais de AIDS;
- Meteorologia: temperatura diária; registro de marés.

## Objetivo

### Principais objetivos

- Compreender o mecanismo gerador da série;
- Predizer o comportamento futuro da série.

### Compreender o mecanismo da série possibilita

- Descrever efetivamente o comportamento da série;
- Encontrar periodicidades na série;
- Obter razões para o comportamento da série;
- Controlar a trajetória da série.

---

# Fenômenos Típicos

## Principais características

### Tendência

- Efeito de longo prazo na média;
- Especificação de longo prazo é difícil.

### Sazonalidade

- Efeitos ligados a variações periódicas (semanal, mensal, anual).

### Ruído

- Variações provocadas por uma variável aleatória;
- Geralmente sem relação temporal.

## Decomposição

Uma das tarefas mais importantes em séries temporais é identificar essas componentes visando a decomposição da série estudada.

---

# Modelos de Séries Temporais

## Objetivo

- Selecionar um modelo probabilístico adequado para os dados;
- Cada observação $x_t$ é considerada resultado de uma variável aleatória $X_t$.

## Modelos com média zero

- Ruído i.i.d.;
- Processo binário;
- Random Walk;
- Modelos com tendência e sazonalidade.

---

## Ruído i.i.d.

### Características

- Modelo mais simples;
- Sem tendência e sazonalidade;
- Observações independentes e identicamente distribuídas;
- Média zero;
- Não existe dependência entre observações.

### Observação

Apesar de não ser interessante para predição, é importante para construção de modelos mais complexos.

### Ruído branco gaussiano

Ruído i.i.d. com distribuição normal, média zero e variância $\sigma^2$.

---

## Processo Binário

As observações assumem apenas dois valores:

$$
P(X_t = 1) = p
$$

$$
P(X_t = -1) = 1 - p
$$

---

## Random Walk

### Características

- Conhecido como “caminhada do bêbado”;
- Passos consecutivos em direções aleatórias;
- Soma cumulativa de variáveis aleatórias i.i.d.

$$
S_t = X_1 + X_2 + \dots + X_t
$$

---

## Tendência e Sazonalidade

### Tendência

Mudança sistemática na série temporal que não aparenta periodicidade.

### Sazonalidade

Comportamento que se repete periodicamente.

---

# Modelos

## Modelo com tendência

$$
X_t = m_t + Y_t
$$

Onde:

$$
m_t = a_0 + a_1 \cdot t
$$

Ajustado minimizando:

$$
\sum_{t=1}^{n}(x_t - m_t)^2
$$

---

## Modelo com sazonalidade

$$
X_t = s_t + Y_t
$$

Onde:

$$
s_t = \alpha_0 + \sum_{j=1}^{k}(a_j\cos(\lambda_j t) + b_j\sin(\lambda_j t))
$$

- $a_j$ e $b_j$: parâmetros desconhecidos;
- $\lambda_j$: frequências.

---

# Abordagem para Modelagem

## Etapas

- Plotar a série;
- Analisar:
  - Tendência;
  - Sazonalidade;
  - Alterações abruptas;
  - Outliers.

## Objetivo

Remover tendência e sazonalidade para obter resíduos estacionários.

---

# Processo Estacionário

## Definição

Processo em equilíbrio estatístico cujas propriedades não variam no tempo.

### Média

$$
\mu_x(t) = E(X_t)
$$

### Covariância

$$
\gamma_x(t+h,t)=E[(X_{t+h}-\mu_x(t+h))(X_t-\mu_x(t))]
$$

## Processo fracamente estacionário

- Média constante;
- Variância constante;
- Covariância depende apenas da defasagem $h$.

---

# Função de Autocorrelação

## Autocovariância

$$
\gamma_x(h)=cov(X_{t+h},X_t)
$$

## Autocorrelação

$$
\rho_x(h)=\frac{\gamma_x(h)}{\gamma_x(0)}
$$

---

# Correlograma

## Objetivo

Analisar autocorrelações em diversas defasagens.

## Utilidade

- Verificar aleatoriedade;
- Detectar tendência;
- Detectar sazonalidade;
- Avaliar resíduos de modelos.

---

# Análise de Séries Temporais

## Modelo clássico de decomposição

$$
X_t = m_t + s_t + Y_t
$$

Onde:

- $m_t$: tendência;
- $s_t$: sazonalidade;
- $Y_t$: ruído estacionário.

---

# Eliminação da Tendência

## Métodos

- Médias móveis;
- Suavização exponencial;
- Eliminação de alta frequência;
- Ajuste polinomial.

---

# Eliminação de Tendência e Sazonalidade

## Procedimento

1. Estimar tendência;
2. Estimar sazonalidade;
3. Remover sazonalidade:

$$
d_t = x_t - \hat{s_t}
$$

4. Reajustar tendência;
5. Remover tendência:

$$
\hat{Y_t} = x_t - \hat{m_t} - \hat{s_t}
$$

---

# Predição

## Modelo ARIMA

**Autoregressive Integrated Moving Average**

### Componentes

- **AR**: Auto Regression;
- **I**: Integrated;
- **MA**: Moving Average.

---

# ARIMA

## Representação

$$
ARIMA(p,d,q)
$$

Onde:

- $p$: ordem autorregressiva;
- $d$: grau de diferenciação;
- $q$: ordem da média móvel.

---

# Referências

- http://www.dme.ufrj.br/dani/pdf/slidespartefrequentista.pdf
- https://www.vooo.pro/insights/guia-completo-para-criar-time-series-com-codigo-em-python/
- https://www.cin.ufpe.br/psgmn/Series%20Temporais/Aula_01.pdf
- https://www.machinelearningplus.com/time-series/arima-model-time-series-forecasting-python/

---

# Próxima aula

Recomendação de Modelos