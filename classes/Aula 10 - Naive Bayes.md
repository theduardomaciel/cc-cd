# Ciência de Dados — Classificador Naive Bayes

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Teorema de Bayes
- Classificador Naive Bayes
- Limitações
- Aplicações

---

# Teorema de Bayes

## Dependência e Independência

Dois eventos $E$ e $F$ são dependentes se:

- Sabendo algo sobre um dos eventos;
- Saberemos algo sobre o outro.

### Exemplos

- Dependentes: estar doente e possuir um sintoma;
- Independentes: lançamento de dados honestos.

---

## Probabilidade Condicional

### Eventos dependentes

$$
P(E,F) = P(E|F)P(F)
$$

$$
P(F,E) = P(F|E)P(E)
$$

### Eventos independentes

$$
P(E|F) = P(E)
$$

$$
P(F|E) = P(F)
$$

$$
P(E,F) = P(E)P(F)
$$

---

## Teorema de Bayes

$$
P(c|D) = \frac{P(D|c)P(c)}{P(D)}
$$

Onde:

- $P(c)$: probabilidade a priori da hipótese $c$
- $P(D)$: probabilidade a priori dos dados de treinamento
- $P(c|D)$: probabilidade de $c$ dado $D$
- $P(D|c)$: probabilidade de $D$ dado $c$

### Observações

- $P(c|D)$ é chamada de probabilidade a posteriori;
- Reflete a influência dos dados de treinamento;
- A probabilidade a priori é independente dos dados.

---

## Exemplo Médico

Dados:

- $P(doença) = 0,01\%$
- $P(teste|doença) = 99\%$

Deseja-se calcular:

$$
P(doença|teste)
$$

Aplicando Bayes:

$$
P(D|T) =
\frac{P(T|D)P(D)}
{P(T|D)P(D)+P(T|\neg D)P(\neg D)}
$$

Resultado aproximado:

$$
0,98\%
$$

---

# Métodos Bayesianos

## Importância

### 1. Algoritmos práticos de aprendizagem

- Combinam conhecimento prévio com dados observados;
- Requerem probabilidades a priori.

### 2. Estrutura conceitual útil

- Pode ser usada para avaliar outros algoritmos.

---

# Classificador Naive Bayes

## Ideia Principal

Queremos encontrar a classe mais provável:

$$
c_{MAP} = \arg\max_{c \in C} P(c|D)
$$

Aplicando Bayes:

$$
c_{MAP} =
\arg\max_{c \in C}
\frac{P(D|c)P(c)}{P(D)}
$$

Como $P(D)$ é constante:

$$
c_{MAP} =
\arg\max_{c \in C}
P(D|c)P(c)
$$

---

## Maximum Likelihood (ML)

Se todas as classes forem igualmente prováveis:

$$
P(c_i)=P(c_j)
$$

Então:

$$
c_{ML} =
\arg\max_{c \in C} P(D|c)
$$

---

# Exemplo — Diagnóstico Médico

Classes:

- Possui H1N1
- Não possui H1N1

Resultados do exame:

- Positivo (+)
- Negativo (-)

Dados:

- Apenas 0,8% da população possui a doença;
- Exame positivo correto: 98%;
- Exame negativo correto: 97%.

### Aplicando Bayes

$$
P(+|H1N1)P(H1N1)
=
0,98 \times 0,008
=
0,0078
$$

$$
P(+|\neg H1N1)P(\neg H1N1)
=
0,03 \times 0,992
=
0,0298
$$

Resultado:

$$
c_{MAP} = \neg H1N1
$$

---

# Classificador Ótimo de Bayes

Para uma nova instância $d$:

$$
\hat{c} =
\arg\max_{c_j \in C}
P(c_j|d)
$$

Qualquer sistema que utiliza essa regra é chamado de:

- Classificador ótimo de Bayes.

---

# Limitações Práticas

- Difícil estimar todas as probabilidades condicionais;
- Necessidade de muitos dados;
- Conhecimento da distribuição de probabilidade;
- Probabilidades a priori podem não refletir a população real.

---

# Naive Bayes

## Quando usar?

- Conjunto de treinamento moderado ou grande;
- Atributos aproximadamente independentes condicionalmente.

### Aplicações

- Diagnóstico médico;
- Classificação textual.

---

## Estrutura do Problema

Nova instância:

$$
<a_1, a_2, \dots, a_n>
$$

Deseja-se prever a classe mais provável.

---

## Formulação

$$
c_{MAP} =
\arg\max_{c_j \in C}
P(c_j|a_1,a_2,\dots,a_n)
$$

Aplicando Bayes:

$$
c_{MAP} =
\arg\max_{c_j \in C}
P(a_1,a_2,\dots,a_n|c_j)P(c_j)
$$

---

## Suposição Naive

Assume independência condicional:

$$
P(a_1,a_2,\dots,a_n|c_j)
=
\prod_{i=1}^{n} P(a_i|c_j)
$$

---

## Classificador Naive Bayes

$$
\hat{c}_{NB} =
\arg\max_{c \in C}
P(c_j)
\prod_{i=1}^{n}
P(a_i|c_j)
$$

As probabilidades são aprendidas a partir das frequências no conjunto de treinamento.

---

# Limitações

## Independência condicional

A hipótese:

$$
P(a_1,\dots,a_n|c_j)
=
\prod_{i=1}^{n} P(a_i|c_j)
$$

muitas vezes é falsa.

Mesmo assim, o método costuma funcionar bem.

---

## Problema de Probabilidade Zero

Se:

$$
P(a_i|c_j)=0
$$

então:

$$
P(c_j)\prod P(a_i|c_j)=0
$$

### Solução: suavização Bayesiana

$$
P(a_i|c_j)
\leftarrow
\frac{n_c + mp}{n+m}
$$

Onde:

- $n$: exemplos com $c=c_j$
- $n_c$: exemplos com $c=c_j$ e $a=a_i$
- $p$: estimativa a priori
- $m$: peso da estimativa

---

# Aplicações

## Tempo real

- Algoritmo rápido.

## Multiclasse

- Funciona bem com múltiplas categorias.

## Classificação de textos

- Spam
- Análise de sentimento
- Classificação documental

## Sistemas de recomendação

- Filtragem colaborativa.

---

# Exemplo — Classificação de Texto

## Objetivos

- Classificar notícias;
- Classificar páginas web.

---

## Representação

Cada posição do texto é tratada como um atributo.

---

## Fórmula

$$
P(doc|c_j)
=
\prod_{i=1}^{length(doc)}
P(a_i=w_k|c_j)
$$

Assumindo:

$$
P(a_i=w_k|c_j)
=
P(a_m=w_k|c_j)
$$

---

# Algoritmo

1. Construir o vocabulário;
2. Calcular:
   - $P(c_j)$
   - $P(w_k|c_j)$

---

## Estimativas

$$
P(c_j)=\frac{|docs_j|}{|Examples|}
$$

$$
P(w_k|c_j)=
\frac{n_k+1}{n+|Vocabulary|}
$$

---

# Resultados

- Precisão aproximada: 89%.

---

# Resumo

## Métodos Bayesianos

- Utilizam conhecimento prévio;
- Calculam probabilidades a posteriori.

## Naive Bayes

- Assume independência condicional;
- Simples;
- Eficiente;
- Pode produzir bons resultados.

---

# Referências

- http://www.eletrica.ufpr.br/ufpr2/professor/36/TE808/5-NaiveBayes-AM.pdf
- Mitchell T. *Machine Learning*. McGraw-Hill, 1997. Capítulo 6.

---

# Próxima Aula

Regressão