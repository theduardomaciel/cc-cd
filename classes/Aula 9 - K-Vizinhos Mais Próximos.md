
**Disciplina:** Ciência de Dados — UFAL  
**Professor:** Bruno Pimentel  
**Tags:** #machine-learning #classificação #aprendizagem-supervisionada #knn

---

## Conceito Central

O K-NN é um método de **aprendizagem baseada em instâncias** (instance-based learning). Ao invés de construir um modelo explícito, ele simplesmente armazena os exemplos de treinamento e classifica novas instâncias com base na semelhança com os dados já vistos.

> "Instâncias similares tendem a pertencer à mesma classe."

---

## Aprendizagem Baseada em Instâncias

- O aprendizado consiste apenas em **armazenar os exemplos de treinamento**
- O conjunto de dados é representado como: $D = {(x_1, c_1), (x_2, c_2), \ldots, (x_n, c_n)}$
    - $x_i = (x_{i1}, x_{i2}, \ldots, x_{ip})$ → instância com $p$ atributos
    - $c_i$ → classe da instância $x_i$
- É um método **não paramétrico**: não assume forma conhecida para a distribuição dos dados
- Constrói uma **aproximação local** da função alvo para cada nova instância

### Desvantagens

- Alto custo computacional no momento da classificação
- O custo aumenta proporcionalmente ao número de exemplos de treinamento

---

## Algoritmo K-NN

### Treinamento

```
Para cada (x, c) no conjunto de treinamento:
    Adicionar (x, c) à lista training_examples
```

### Classificação

Dada uma instância $x_t$ a classificar:

1. Calcular $d(x_t, x_i)$ para todo $i = 1, \ldots, n$
2. Selecionar os $k$ vizinhos mais próximos: $x_1, \ldots, x_k$
3. Retornar a classe mais frequente (votação):

$$f(x_t) = \arg\max_{c \in C} \sum_{i=1}^{k} I(c, f(x_i))$$

onde $I(a, b) = 1$ se $a = b$, e $0$ caso contrário.

---

## Distância Euclidiana

Dadas duas instâncias $x_a$ e $x_b$ com $p$ atributos:

$$d(a, b) = \sqrt{\sum_{j=1}^{p} (x_{aj} - x_{bj})^2}$$

---

## Complexidade Computacional

Para $n$ exemplos de treinamento com $p$ dimensões e $k = 1$:

|Operação|Custo|
|---|---|
|Inspecionar cada exemplo|$O(n)$|
|Calcular distância Euclidiana|$O(p)$|
|Reter o mais próximo|$O(1)$|
|**Total**|**$O(np)$**|

---

## Escolha do Valor de K

O valor de $k$ impacta diretamente o desempenho do modelo:

- **$k$ pequeno** (ex: $k=1$): overfitting — o modelo "memoriza" os dados de treino (erro de treino = 0)
- **$k$ grande**: underfitting — fronteiras de decisão muito suaves

### Métodos para escolher k

- **Hold-out:** separar parte dos dados para validação e testar diferentes valores de $k$
- **Cross-validation:** avaliar desempenho médio em múltiplas partições dos dados
- **Otimização:** busca automatizada pelo melhor $k$

---

## Variações

### Distância Ponderada

Em vez de voto simples, cada vizinho contribui com peso inversamente proporcional à distância:

$$f(x_t) = \arg\max_{c \in C} \sum_{i=1}^{k} w_i \cdot I(c, f(x_i))$$

$$w_i = \frac{1}{d(t, i)^2}$$

- Vizinhos mais próximos têm **maior influência**
- Permite considerar **todos** os exemplos de treinamento (distâncias grandes → peso muito pequeno)
- **Desvantagem:** mais lento

### Método de Hart (Condensação)

Reduz o conjunto de treinamento sem perder informação relevante:

1. Inicia com uma instância do conjunto original
2. Move para o novo conjunto toda instância que for **classificada incorretamente** pelo classificador 1-NN atual
3. Repete até que o conjunto se estabilize com **zero erros**

> Seleciona principalmente amostras próximas à **fronteira de decisão** entre as classes.

---

## Vantagens e Desvantagens

|Vantagens|Desvantagens|
|---|---|
|Modela funções alvo complexas com aproximações locais|Alto tempo de processamento na classificação|
|Nunca perde a informação dos exemplos de treinamento|Requer definição de uma métrica de distância adequada|
|Não paramétrico (funciona com qualquer distribuição)|Sensível a atributos irrelevantes ou com escalas diferentes|

---

## Aplicação: Localização Indoor com RFID

O K-NN pode ser usado para estimar a posição de etiquetas RFID em ambientes internos, onde sinais GPS sofrem interferência.

**Ideia:** Usar a força do sinal como "coordenada" e encontrar as etiquetas de referência mais próximas.

**Distância entre etiquetas:**

$$E_r^j = \sqrt{\sum_{i=1}^{n} (\theta_i^r - S_i^j)^2}$$

**Peso de cada vizinho:**

$$W_i^j = \frac{1/(E_i^j)^2}{\sum_{c=1}^{k} 1/(E_c^j)^2}$$

**Estimativa final de posição:**

$$(x, y)^j = \sum_{c=1}^{k} W_c^j \cdot (x_c, y_c)$$

---

## Resumo

```
K-NN
├── Armazena todos os exemplos de treino
├── Classifica por votação dos k vizinhos mais próximos
├── Usa distância Euclidiana (padrão)
├── Sem fase de treino explícita → custo na predição
├── Variações
│   ├── Distância ponderada (peso = 1/d²)
│   └── Método de Hart (condensação do conjunto)
└── Hiperparâmetro principal: k (escolher por cross-validation)
```

---

## Próxima Aula

- [[Aula 10 - Naive Bayes]]

## Referências

- http://www.eletrica.ufpr.br/ufpr2/professor/36/TE808/6-kNN-AM.pdf
- https://www.ic.unicamp.br/~afalcao/mo445/aula13.pdf