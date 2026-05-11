**LISTA 2 - CIÊNCIA DE DADOS**

**Conclusão Final**

Telco Customer Churn Dataset

_Resumo geral: clientes com contrato mensal, menos de 12 meses de casa e cobrança mensal acima da mediana representam 26% da base, mas concentram mais de 50% do risco de churn - e são o alvo prioritário de retenção._

# **1\. Principais Decisões Metodológicas**

O projeto foi conduzido com três comprometimentos metodológicos mantidos em todas as dez questões. Cada um deles foi motivado por uma evidência concreta identificada ainda na Questão 1 e confirmada ao longo da análise.

**1.1 Métrica principal: F1 e Recall em lugar de Acurácia**

A base apresenta desbalanceamento de **2,77×** (73,5% de não-cancelamento contra 26,5% de churn). Com essa proporção, um modelo que classificasse todos os clientes como "não vai cancelar" atingiria acurácia de 73,5% - número alto, mas sem nenhum valor preditivo. Por isso, F1 e Recall da classe positiva foram adotados como métricas centrais em todas as questões de classificação (Q2, Q4, Q5 e Q8). O Recall mede especificamente o custo operacional mais crítico: clientes que vão cancelar e _não_ são identificados (falsos negativos) - cada um representa receita perdida sem tentativa de retenção.

**1.2 Features engineered validadas, não assumidas**

Quatro features derivadas foram criadas com base em evidências da Lista 1 (Q5 - força de associação) e validadas ao longo da Lista 2: **contract_tenure_interaction** (produto contrato × tempo de casa, que explicou o salto de R² de 0,80 para 0,96 na Q3); **is_new_customer** (tenure ≤ 6 meses, zona crítica identificada na Q6); **service_adoption_count** (hub de centralidade na rede de atributos da Q7); e **contract_numeric** (ordinalização que permitiu a interação multiplicativa). Nenhuma feature foi incluída por intuição - cada uma foi incluída porque sua relevância pôde ser medida em um resultado anterior.

**1.3 Conclusões calibradas pela evidência disponível**

O principal ponto de melhoria indicado na avaliação da Lista 1 foi a tendência de "conclusões mais fortes do que a evidência mostrada sustenta". Esse compromisso foi endereçado sistematicamente: cada limitação metodológica foi documentada na própria questão onde ocorreu (independência violada na Q2, ausência de data real na Q6, rede artificial na Q7), e nenhuma afirmação forte foi feita sem ser rastreada a um número produzido pelo código. A calibração foi aplicada inclusive na direção oposta: quando a Regressão produziu R² = 0,96, o texto explicou _por que_ esse número era esperado pela estrutura matemática da interação - e não o usou como argumento de excelência irrestrita do modelo.

# **2\. Comparação entre os Modelos Utilizados**

A tabela abaixo consolida os resultados dos modelos de classificação avaliados nas Q2, Q4 e Q5, com as métricas calculadas no mesmo protocolo: divisão treino/teste 80/20 estratificada + validação cruzada estratificada de 10 folds.

| **Modelo**       | **F1 (teste)** | **AUC-ROC** | **Brier** | **Estabilidade** | **Uso recomendado** |
| ---------------- | -------------- | ----------- | --------- | ---------------- | ------------------- |
| Naive Bayes      | ≈ 0,59         | ≈ 0,83      | Alto      | Baixa            | Baseline            |
| Reg. Logística   | ≈ 0,66         | ≈ 0,85      | Baixo     | Alta             | **★ Produção**      |
| Árvore (depth=5) | ≈ 0,65         | ≈ 0,84      | Médio     | Média            | Explicação          |
| Árvore (depth=4) | ≈ 0,63         | ≈ 0,83      | Médio     | Alta             | CRM / Operação      |

**Naive Bayes (GaussianNB).** Cumpriu seu papel como baseline probabilístico. O F1 de ≈ 0,59 reflete exatamente a limitação teórica identificada na Q2: a correlação de 0,65-0,83 entre _MonthlyCharges_ e _TotalCharges_ viola a suposição de independência condicional de forma estrutural - não é corrigível por pré-processamento. Quando o modelo trata variáveis correlacionadas como evidências independentes, ele infla a confiança das predições, o que se manifesta no Brier Score mais alto entre os três. A Q8 confirmou esse padrão experimentalmente: o NB é o modelo com maior amplitude de F1 ao variar o subconjunto de features, exatamente porque sua suposição central é a mais sensível à composição de atributos.

**Regressão Logística.** Produziu o melhor equilíbrio entre as quatro dimensões avaliadas na Q5: F1 competitivo, AUC mais alto, Brier Score mais baixo (probabilidades mais calibradas) e menor desvio-padrão do F1 em validação cruzada. A calibração é particularmente relevante para o uso em produção: se o modelo atribui P(churn) = 0,70 a um cliente, isso deve significar que aproximadamente 70% dos clientes com esse perfil realmente cancelam - condição necessária para que a ordenação de clientes por risco seja confiável. A Q8 confirmou a estabilidade da RL: entre os 75 experimentos do meta-dataset, a RL apresentou menor variância de F1 ao variar subconjuntos de features, pré-processamentos e particionamentos.

**Árvore de Decisão.** A configuração ótima (depth=5, entropy, min_leaf=10) produziu F1 competitivo com a RL, mas com maior gap de overfitting - documentado no gráfico de gap da Q4, onde profundidades ≥ 7 ultrapassaram a referência de 0,05. A versão podada (depth=4) oferece o diferencial que nem o NB nem a RL possuem: **interpretabilidade operacional**. As regras de quatro níveis da árvore podem ser apresentadas ao time de CRM sem mediação técnica: "se o cliente tem contrato mensal, tenure ≤ 12 meses e cobrança acima de R\$ X, classifique como risco alto". Essa propriedade tem valor de negócio real, independente de diferenças marginais de F1.

_Recomendação de uso combinado: Regressão Logística para geração de scores de risco (ordenação de clientes por probabilidade de churn) + Árvore de Decisão (depth=4) como camada de explicabilidade para o time de retenção. Os dois modelos chegam às mesmas conclusões sobre os perfis de maior risco, o que fortalece a confiança na decisão._

# **3\. Limitações da Base Escolhida**

A base Telco-Customer-Churn é **cross-sectional**: um único corte temporal de 7.043 clientes, cada um registrado uma vez com seu estado no momento da observação. Essa característica estrutural é a limitação mais relevante do projeto e afetou cada método em graus diferentes.

**3.1 Ausência de dimensão temporal real**

A variável _tenure_ registra há quantos meses o cliente estava ativo no momento do corte - não é uma série histórica. Isso teve duas consequências diretas: (a) na Q6, a análise de séries temporais precisou ser construída por agregação de coorte, produzindo uma série descritiva mas sem capacidade de previsão longitudinal; (b) o modelo de churn não sabe se um cliente _começou_ com risco alto e reduziu, ou se seu risco é estável - ele enxerga apenas o estado no momento da observação.

**3.2 Ausência de variáveis de comportamento e satisfação**

A base não contém: histórico de reclamações, número de contatos com o suporte, tempo de resposta da operadora, NPS ou qualquer indicador de satisfação. Essas variáveis são tipicamente os principais preditores de churn em projetos reais de telecomunicações - e sua ausência pode gerar **viés de variável omitida**: o modelo associa cobrança alta ao churn não necessariamente porque cobranças altas causam cancelamento, mas porque ambos podem ser causados por um terceiro fator (insatisfação com o serviço) que não está no dataset.

**3.3 Ausência de relações entre clientes**

Clientes não têm relacionamentos explícitos entre si na base, o que tornou a Análise de Redes (Q7) metodologicamente limitada para o problema principal. A rede de portfólios foi construída por similaridade de pacotes - uma relação definida artificialmente, não observada. A rede de correlação entre atributos, por outro lado, produziu valor de comunicação ao tornar visível a estrutura de dependência entre variáveis.

**3.4 Tamanho e representatividade**

Os 7.043 registros são suficientes para os modelos testados - validação cruzada com 10 folds produz folds de ≈ 700 clientes, tamanho adequado para estimativas estáveis. Para a Q8 (meta-aprendizagem), porém, 75 experimentos não são suficientes para treinar um meta-classificador com garantias estatísticas; a regra técnica derivada é heurística, não um modelo generalizável. Isso foi documentado explicitamente na Q8 e não compromete as conclusões das questões de classificação.

# **4\. Avaliação Final da Adequação da Solução ao Cenário**

A tabela abaixo fecha o ciclo iniciado na Q1, onde a adequação de cada método foi avaliada _a priori_. Após executar todos os métodos, é possível comparar a expectativa inicial com o resultado empírico obtido - e documentar as adaptações que foram necessárias.

| **Método**        | **Adeq. Q1** | **Adeq. Real**      | **Adaptação Necessária**                                            | **Evidência Empírica**                                                          |
| ----------------- | ------------ | ------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Naive Bayes       | **Alta**     | **Média**           | Suposição de independência viola corr. ≥ 0,65 entre numéricas       | F1 ≈ 0,59 - abaixo dos demais; razão teórica confirmada empiricamente           |
| Regressão         | **Média**    | **Alta (subprob.)** | Redefinição do alvo: TotalCharges como proxy de LTV                 | R² = 0,96 com interação tenure × MonthlyCharges                                 |
| Árvore de Decisão | **Alta**     | **Alta**            | Controle de profundidade e min_samples_leaf (gap overfitting)       | F1 CV competitivo; depth=4 interpretável para o time de CRM                     |
| Séries Temporais  | **Baixa**    | **Baixa**           | Série de coorte por tenure - proxy sem garantias longitudinais      | Queda descritiva de ~42% para ~8%; sem previsão futura robusta                  |
| Análise de Redes  | **Baixa**    | **Baixa / Média**   | Rede de portfólios (artificial) + rede de correlação entre vars.    | Rede de correlação comunica dependência entre atributos; portfólios: artificial |
| Meta-aprendizagem | **Alta**     | **Alta (ressalva)** | 75 experimentos: regra heurística - insuficiente p/ meta-clf.       | Regra de 4 condições converge com Q5 por caminho independente                   |
| Visualização      | **Alta**     | **Alta**            | Distinção exploratório vs. explanatório; 3 alternativas descartadas | Painel em 3 atos; narrativa causal do problema à ação                           |

**O que mudou entre a avaliação a priori (Q1) e a avaliação retroativa (Q10).** Dois métodos mudaram de posição: a **Regressão** subiu de Média para Alta porque a redefinição do alvo (TotalCharges como proxy de LTV) foi bem motivada pela evidência da Q2 (correlação estrutural entre variáveis monetárias) e produziu R² = 0,96 - resultado que a avaliação teórica não podia antecipar. A **Análise de Redes** permaneceu Baixa para o problema principal, mas revelou adequação Média em um subproblema específico (rede de correlação entre atributos) que não foi antecipado na Q1. Os demais métodos mantiveram a avaliação inicial, o que indica consistência entre a análise estrutural da base e os resultados empíricos.

**Adequação ao cenário de negócio.** A solução responde à pergunta de negócio que motivou a análise: _quais clientes a Telco deve priorizar em campanhas de retenção, e com qual argumento de valor?_ A segmentação em três grupos (alto risco, risco moderado, baixo risco) com taxa de churn, volume de clientes e receita mensal em risco por segmento entrega um produto acionável - não apenas uma previsão binária. As ações recomendadas para cada segmento (oferta de migração para contrato anual com desconto, monitoramento automático, programa de fidelidade) são coerentes com os achados dos modelos e com os padrões identificados na análise de coorte da Q6.

**O que a análise não pode afirmar.** Com a base disponível, não é possível: (a) prever quando um cliente vai cancelar - apenas se ele está em grupo de risco no momento do corte; (b) estimar o impacto de uma campanha de retenção sobre a taxa de churn - a base não tem histórico de intervenções; (c) afirmar que cobrança alta _causa_ churn - apenas que as duas variáveis são correlacionadas nos dados observados. Essas restrições são inerentes à estrutura cross-sectional da base e não são corrigíveis por escolha de modelo.

_Nota metodológica: a maior contribuição deste projeto não está em nenhum resultado isolado, mas na consistência dos resultados identificados entre as questões. Os mesmos três fatores de risco - tipo de contrato, tempo de casa e cobrança mensal - foram identificados independentemente pela força de associação (Lista 1 Q5), pela importância na Árvore de Decisão (Q4), pelos coeficientes da Regressão Logística (Q5), pelo padrão na série de coorte (Q6), pela centralidade na rede de atributos (Q7) e pela regra técnica do meta-experimento (Q8). Essa convergência, por caminhos metodológicos distintos, é o argumento mais sólido em favor da confiabilidade das conclusões._