<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./.github/cover.png">
  <source media="(prefers-color-scheme: light)" srcset="./.github/cover_light.png">
  <img alt="Ciência de Dados" src="/.github/cover_light.png">
</picture>

# Ciência de Dados - UFAL 2026.1

Repositório com atividades, materiais de estudo e projetos desenvolvidos durante a disciplina de **Ciência de Dados** no curso de Engenharia da Computação da Universidade Federal de Alagoas (UFAL).

## 📋 Estrutura do Repositório

### 📚 `/classes` - Materiais de Aula
Notas e documentos das aulas cobrindo os principais tópicos:

- **Aula 2** - Conceitos de Ciência de Dados
- **Aula 3** - Big Data
- **Aula 5** - Estatística
- **Aula 6** - Pré-processamento de Dados
- **Aula 7** - Aprendizagem de Máquina
- **Aula 9** - K-Vizinhos Mais Próximos (KNN)
- **Aula 10** - Naive Bayes

### 📊 `/data` - Conjuntos de Dados
Bases de dados utilizadas nos exercícios e projetos:

- `HR-Employee-Attrition.csv` - Dados sobre atrito de funcionários
- `Telco-Customer-Churn.csv` - Churn de clientes em telecomunicações
- `Medical_Appointment_No_Shows.csv` - Falta em consultas médicas
- `marketing_campaign.csv` - Dados de campanhas de marketing
- `melb_data.csv` - Dados imobiliários de Melbourne

### 📝 `/listas` - Exercícios Práticos
Notebooks com exercícios e práticas implementadas em Python:

- **lista1.ipynb** - Exercícios introdutórios
- **lista2.ipynb** - Projeto abrangente de Aprendizagem de Máquina com 10 questões cobrindo:
  1. Definição do problema analítico
  2. Naive Bayes
  3. Regressão
  4. Árvore de Decisão
  5. Comparação entre modelos
  6. Séries Temporais
  7. Análise de Redes
  8. Meta-aprendizagem
  9. Visualização de Dados
  10. Consolidação da solução

### 🎯 `/projeto` - Projeto Final
Projeto completo de Ciência de Dados aplicado a dados de reservas hoteleiras, incluindo:
- Análise exploratória de dados
- Pré-processamento e limpeza
- Modelagem com técnicas de Aprendizagem de Máquina
- Testes de hipótese e validação
- Apresentação de resultados e recomendações

## 🛠️ Tecnologias e Bibliotecas

O projeto utiliza as seguintes bibliotecas Python (ver `requirements.txt`):

- **Análise de Dados:** pandas, numpy, scipy
- **Visualização:** matplotlib, seaborn
- **Machine Learning:** scikit-learn
- **Redes:** networkx
- **Jupyter:** jupyter, ipykernel
- E outras dependências auxiliares

## 🚀 Como Usar

### Configuração do Ambiente

1. Clone o repositório:
```bash
git clone <url-do-repositorio>
cd cc-cd
```

2. Crie um ambiente virtual:
```bash
python -m venv .venv
source .venv/Scripts/activate  # Windows
# ou
source .venv/bin/activate  # Linux/Mac
```

3. Instale as dependências:
```bash
pip install -r requirements.txt
```

### Executando os Notebooks

```bash
jupyter notebook listas/lista2.ipynb
```

## 📌 Principais Decisões Metodológicas

- **Validação:** Uso de k-fold cross-validation para robustez
- **Pré-processamento:** Tratamento padronizado de dados antes da modelagem
- **Comparação:** Avaliação sistemática de múltiplas técnicas para cada problema
- **Interpretabilidade:** Priorização de modelos interpretáveis quando possível

## 🎓 Aprendizados Principais

Este repositório demonstra a aplicação prática de técnicas de Ciência de Dados desde a preparação dos dados até a apresentação de resultados, enfatizando:

- A importância do pré-processamento na qualidade dos modelos
- A seleção adequada de algoritmos conforme o problema
- A validação rigorosa e comparação de abordagens
- A comunicação clara dos resultados para stakeholders

## 📚 Referências

- Materiais das aulas de Ciência de Dados - UFAL 2026.1
- Documentação oficial: scikit-learn, pandas, matplotlib
- Boas práticas em relatório científico (SBC - Sociedade Brasileira de Computação)

## 📄 Licença

Este projeto foi desenvolvido como atividade acadêmica na disciplina de Ciência de Dados (2026.1).
