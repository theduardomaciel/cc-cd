# Ciência de Dados — Métodos Baseados em Árvores e Regras

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Introdução
- Árvore de decisão
- Ganho de informação
- Overfitting

---

# Introdução

## Indução

Exemplo:

- Dia 1: faz sol em Maceió;
- Dia 2: faz sol em Maceió;
- Dia 3: faz sol em Maceió;
- Dia 4: faz sol em Maceió.

Pergunta:

- Dia 5?

---

# Aprendizagem Indutiva

## Hipótese indutiva

"Todo dia faz sol em Maceió."

---

## Conhecimento em extensão

- Exemplos;
- Percepção-ação;
- Características-conceito.

---

## Conhecimento em intenção

- Regras;
- Definições.

---

# Categorias

## Incremental

- Atualiza hipótese a cada novo exemplo;
- Mais flexível;
- Ordem importa.

## Não incremental

- Usa todos os exemplos;
- Mais eficiente;
- Mais prática.

---

# Árvores de Decisão

## Características

- Aprendizagem indutiva não incremental;
- Fácil implementação;
- Representação atributo-valor.

---

## Componentes

- Nó: teste de atributo;
- Ramo: valor do teste;
- Folha: decisão final.

---

# Problemas Apropriados

- Variáveis categóricas;
- Resposta discreta;
- Dados incompletos;
- Dados com ruído.

---

# Algoritmo ID3

Enquanto o critério de parada não for satisfeito:

1. Escolher o melhor atributo;
2. Criar ramos;
3. Ordenar exemplos.

---

# Variáveis Contínuas

Transformação em variável booleana:

$$
A_c=
\begin{cases}
Verdadeiro,& A<c\\
Falso,& A\ge c
\end{cases}
$$

---

# Entropia

## Definição

$$
Entropia(S)=
-p_+\log_2(p_+)
-p_-\log_2(p_-)
$$

Onde:

- $p_+$: proporção positiva;
- $p_-$: proporção negativa.

---

# Exemplos de Entropia

$$
Entropia([5^+,5^-])=1.0
$$

$$
Entropia([2^+,1^-])=0.9183
$$

$$
Entropia([3^+,4^-])=0.9852
$$

---

# Ganho de Informação

## Fórmula

$$
Ganho(S,A)=
Entropia(S)
-
\sum_{v\in Valores(A)}
\frac{|S_v|}{|S|}
Entropia(S_v)
$$

---

# Exemplo

## Resultados

$$
Ganho(S,Temp)=0.2781
$$

$$
Ganho(S,Feriado)=0.0349
$$

Logo:

- Temperatura é o melhor atributo.

---

# Critérios de Parada

- Profundidade;
- Número de folhas;
- Número de instâncias;
- Folhas puras.

---

# Overfitting

## Definição

Overfitting ocorre quando:

- O modelo se ajusta demais ao conjunto de treinamento;
- Generaliza mal para novos dados.

---

# Holdout

Separação em:

- Treinamento;
- Teste.

---

# Como Evitar Overfitting

## Alternativas

1. Interromper crescimento;
2. Crescer totalmente e podar.

---

# Técnicas de Poda

## 1. Critical Value Pruning

- Usa valor crítico;
- Remove nós pouco relevantes.

---

## 2. Reduced-Error Pruning

- Compara erro com e sem poda;
- Continua enquanto a poda for vantajosa.

---

## 3. Cost-Complexity Pruning

- Considera:
  - erro;
  - número de folhas.

---

# Comparação

## Critical Value Pruning

### Vantagem

- Gera várias árvores.

### Desvantagem

- Dependente do valor crítico.

---

## Reduced-Error Pruning

### Vantagem

- Simples e eficiente.

### Desvantagem

- Pode podar excessivamente.

---

## Cost-Complexity Pruning

### Vantagem

- Mais refinado.

### Desvantagem

- Alto custo computacional.

---

# Referências

- Tom Mitchell. *Machine Learning*. McGraw-Hill, 1997.
- Patil, Wadhai & Gokhale. *Evaluation of Decision Tree Pruning Algorithms for Complexity and Classification Accuracy*. International Journal of Computer Applications, 2010.

---

# Próxima Aula

Redes Neurais