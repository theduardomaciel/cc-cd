# Ciência de Dados - Recomendação de Modelos

**Bruno Pimentel**  
brunopimentel@ic.ufal.br

---

# Sumário

- Introdução
- Estudos recentes
- Recomendação de modelos
- Aplicações

---

# Mineração de Dados

## Objetivos

- Extração de informação;
- Automatização da descoberta de padrões;
- Uso de aprendizagem de máquina.

## Problema

Existem diversos algoritmos disponíveis e a escolha correta é importante.

---

# No Free Lunch

## Ideia principal

Nenhum algoritmo é melhor para todos os problemas.

## Consequências

- Diferentes algoritmos funcionam melhor em diferentes contextos;
- O desempenho médio tende a ser equivalente considerando todos os problemas possíveis.

---

# Abordagem Tradicional

## Processo

1. Selecionar subconjunto de algoritmos;
2. Aplicar algoritmos;
3. Avaliar desempenho;
4. Ajustar configurações.

## Desvantagens

- Dependência de especialistas;
- Alto custo;
- Processo demorado.

---

# Motivação

## Objetivos

- Reduzir número de algoritmos testados;
- Otimizar experimentação;
- Melhorar seleção automática.

---

# Estudos Recentes

- Recomendação de hiperparâmetros;
- Transferência de conhecimento;
- Otimização de pipelines;
- Predição de desempenho;
- Recomendação de modelos.

---

# Recomendação de Modelos

## Objetivo

Selecionar automaticamente algoritmos adequados para um problema.

---

# Modelagem Formal

Para um problema $x \in P$:

- Extrair características $f(x)$;
- Encontrar mapeamento $S(f(x))$;
- Selecionar algoritmo $\alpha \in A$;
- Maximizar desempenho $y(\alpha(x))$.

---

# Procedimento

## Etapas

1. Aquisição de problemas;
2. Avaliação dos algoritmos;
3. Extração de características;
4. Criação de meta-dados;
5. Aprendizado do meta-modelo;
6. Recomendação de algoritmos.

---

# Caracterização de Bases de Dados

## Objetivo

Identificar propriedades que afetam desempenho dos modelos.

---

# Tipos de Caracterização

## Direta

Uso de estatísticas dos dados:

- Número de exemplos;
- Número de atributos;
- Número de classes;
- Correlação;
- Assimetria;
- Curtose;
- Entropia.

---

## Landmarking

Uso de algoritmos simples para caracterizar bases.

### Objetivo

Determinar similaridade entre conjuntos de dados.

---

## Via Modelos

Utiliza a estrutura do classificador como representação dos dados.

### Exemplos

- Árvores de decisão.

---

# Medidas de Avaliação

## Exemplos

- AUC;
- Taxa de acerto;
- F-measure;
- Tempo de treinamento.

---

# Formas de Sugestão

## Melhor algoritmo

### Vantagem

- Simples.

### Desvantagem

- Não garante melhor desempenho.

---

## Algoritmos promissores

Sugere algoritmos não significativamente inferiores ao melhor.

---

## Ranking

Exibe algoritmos ordenados por preferência.

---

# Construção da Sugestão

## Objetivo

Relacionar características dos dados ao desempenho dos algoritmos.

## Estratégia

- Criar meta-exemplos;
- Utilizar meta-aprendizado;
- Construir meta-modelos.

---

# Aplicações

## DataRobot

### Características

- Automatiza aprendizado de máquina;
- Criação rápida de modelos;
- Interpretabilidade.

---

## Cloud AutoML

### Objetivo

Permitir treinamento de modelos com pouco conhecimento técnico.

### Produtos

#### Visão

- Análise de imagens;
- Vídeos.

#### Idioma

- Estrutura e significado do texto;
- Tradução automática.

#### Dados estruturados

- Modelos automáticos para dados tabulares.

---

# Referências

- https://www.cin.ufpe.br/~rbcp/souza_JAI_2011.pdf
- https://www.fep.up.pt/docentes/fontes/FCTEGE2008/Publicacoes/T5.pdf
- Japkowicz, Nathalie, and Mohak Shah.

---

# Próxima aula

Projeto