# Ciência de Dados - Análise de Redes Sociais

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Motivação
- Conceitos Básicos
- Análise Estrutural
- Detecção de Comunidades

---

# Motivação

## O que é Rede Social

Rede social é uma estrutura social:

- Composta por pessoas ou organizações;
- Conectadas por relações;
- Compartilham valores e objetivos.

## Exemplos

- Facebook
- Twitter
- Instagram
- LinkedIn

---

# Fonte de Dados

As redes sociais transformaram a forma como nos conectamos.

## Características

- Bilhões de usuários;
- Grande quantidade de informações;
- Fonte rica para análise de dados.

---

# Aplicações

## Marketing

- Identificação de influenciadores;
- Segmentação de público;
- Mensuração de campanhas.

## Ciências Sociais

- Estudo de comportamento;
- Disseminação de informação;
- Formação de comunidades.

## Segurança

- Detecção de ameaças;
- Combate a fraudes.

## Saúde Pública

- Monitoramento de doenças;
- Identificação de grupos de risco.

---

# Principais Técnicas

## Coleta de Dados

- APIs;
- Raspagem de dados;
- Importação de arquivos.

## Técnicas Analíticas

- Análise de centralidade;
- Detecção de comunidades;
- Análise de sentimentos;
- Propagação de informações;
- Visualização de redes.

---

# Conceitos Básicos

## Rede Social e Grafo

Uma rede social pode ser modelada por um grafo.

## Grafo

$$
G = (V,E)
$$

Onde:

- $V$: vértices;
- $E$: arestas.

---

# Matriz de Adjacência

$$
A=[a_{ij}]
$$

Onde:

- $a_{ij}=1$: existe aresta;
- $a_{ij}=0$: não existe aresta.

---

# Tipos de Grafos

## Não direcionados

Arestas sem direção.

## Direcionados

Arestas possuem direção.

## Ponderados

Arestas possuem pesos.

---

# Análise Estrutural

## Objetivo

Investigar a estrutura da rede utilizando métricas de teoria dos grafos.

## Métricas

### Locais

Relacionadas aos indivíduos.

### Globais

Relacionadas à rede inteira.

---

# Métricas Locais

## Centralidade de Grau

$$
C(i)=\frac{\sum_j A_{ij}}{n-1}
$$

Mede quantas conexões um nó possui.

---

## Centralidade de Proximidade

$$
C_{close}(i)=\frac{1}{\sum_j d(i,j)}
$$

Mede proximidade entre nós.

---

## Centralidade de Intermediação

$$
C_{betweenness}(i)=\sum_{s\neq i\neq t}\frac{\sigma_{st}(i)}{\sigma_{st}}
$$

Mede presença nos caminhos mínimos.

---

## PageRank

$$
PR^{(t+1)}(i)=(1-d)+d\sum_{j\in M(i)}\frac{PR^{(t)}(j)}{L(j)}
$$

Onde:

- $d$: fator de amortecimento;
- $M(i)$: nós que apontam para $i$.

---

## Coeficiente de Agrupamento

$$
C(i)=\frac{2E(i)}{k(i)(k(i)-1)}
$$

Mede transitividade das relações.

---

# Métricas Globais

- Clique máximo;
- Média dos caminhos mínimos;
- Diâmetro;
- Coeficiente de agrupamento;
- Centralização.

---

# Detecção de Comunidades

## Objetivo

Identificar grupos de nós fortemente conectados.

---

# Estratégias

## Métodos de Agrupamento

- Particionais;
- Baseados em densidade;
- Hierárquicos.

## Métodos Espectrais

Análise de autovetores de matrizes derivadas da rede.

---

# Agrupamento Particional

## K-Means

### Vantagem

- Eficiência computacional.

### Desvantagem

- Necessidade de definir número de comunidades.

---

# Algoritmos Hierárquicos

## Divisivos

Removem arestas importantes iterativamente.

## Aglomerativos

Maximizam modularidade.

$$
\Delta Q = 2(e_{ij} - a_i a_j)
$$

---

# Métodos Espectrais

## Matriz de modularidade

$$
b^{(g)}_{ij}=a_{ij}+\frac{k_i k_j}{2M}-\delta_{ij}\sum_{u\in g}\left(a_{iu}-\frac{k_i k_u}{2M}\right)
$$

---

# Conclusão

## Importância

- Extração de informações;
- Identificação de comunidades;
- Entendimento da dinâmica das redes.

## Aplicações

- Internet;
- Redes sociais;
- Redes biológicas;
- Redes organizacionais.

## Desafios

- Alto custo computacional;
- Número desconhecido de comunidades.

---

# Referências

- Tsvetovat, M., & Kouznetsov, A. (2011).
- https://github.com/beekal.pdf
- http://www.each.usp.br/digiampietri/SIN5028/
- http://wiki.icmc.usp.br/images/5/5e/ApresentacaoGlendaFabiano.pdf