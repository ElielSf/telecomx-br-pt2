# Relatório de Análise de Evasão de Clientes (Churn)

## 1. Introdução

Este relatório apresenta os resultados da modelagem preditiva de evasão de clientes, desenvolvida com dois modelos de machine learning — **Regressão Logística** e **Random Forest**. O objetivo é identificar os principais fatores que influenciam o cancelamento de serviços e propor estratégias de retenção baseadas nos dados.

---

## 2. Desempenho dos Modelos

| Métrica | Regressão Logística | Random Forest |
|---|---|---|
| Acurácia | 75,0% | 79,9% |
| Precisão | 52,0% | 66,3% |
| Recall | **79,9%** | 50,0% |
| F1-Score | **0,63** | 0,57 |

Ambos os modelos foram ajustados para corrigir problemas identificados na versão inicial:

- A **Regressão Logística** apresentava underfitting, com Recall de 52,9%. Após aplicar `class_weight='balanced'`, o Recall subiu para 79,9%, tornando o modelo mais sensível à detecção de clientes em risco.
- O **Random Forest** apresentava overfitting severo (99,7% no treino vs 78,5% no teste). Após limitar a profundidade das árvores com `max_depth=10` e `min_samples_leaf=5`, a diferença caiu para ~4 pontos percentuais.

Para o contexto de churn, a **Regressão Logística é o modelo recomendado** — Recall alto significa menos clientes em risco passando despercebidos, o que é o objetivo central do negócio.

---

## 3. Fatores que Influenciam a Evasão

### 3.1 Fatores de Risco — aumentam a probabilidade de churn

Ambos os modelos convergiram nos mesmos fatores de risco, o que reforça a confiabilidade dos resultados:

**Contrato mensal** foi o fator de risco mais forte em ambos os modelos. Clientes sem compromisso de longo prazo têm total liberdade para cancelar a qualquer momento, e de fato o fazem com muito mais frequência.

**Internet de fibra óptica** apareceu como fator de risco relevante nos dois modelos. Apesar de ser um serviço premium, esses clientes apresentam maior tendência à evasão — possivelmente por expectativas mais altas em relação à qualidade e suporte, ou por estar em um segmento mais competitivo de mercado.

**Pagamento por cheque eletrônico** foi identificado como sinal de alerta. Esse método de pagamento pode indicar um perfil de cliente menos engajado com a empresa, sem vínculo financeiro automático como cartão de crédito ou débito automático.

**Fatura digital** e **cobrança mensal alta** também contribuem positivamente para o risco de churn, sugerindo que clientes com planos mais caros e sem relacionamento presencial são mais propensos a cancelar.

### 3.2 Fatores de Proteção — reduzem a probabilidade de churn

**Tempo de contrato (`meses_contrato`)** foi a variável mais importante no Random Forest e apresentou coeficiente negativo forte na Regressão Logística. Clientes com mais tempo de casa cancelam muito menos — o vínculo e a familiaridade com o serviço funcionam como âncora de retenção.

**Contrato bienal** reforça essa lógica: clientes com contratos longos apresentam baixíssima taxa de evasão. O compromisso formal de longo prazo reduz a probabilidade de cancelamento de forma significativa.

**Suporte técnico ativo** e **segurança online contratada** apareceram com coeficiente negativo na Regressão Logística, indicando que clientes que utilizam serviços adicionais estão mais integrados ao ecossistema da empresa e tendem a permanecer.

**Cobrança total acumulada** também apresentou coeficiente negativo — clientes com maior valor acumulado são, em geral, clientes antigos, que já demonstraram fidelidade ao longo do tempo.

---

## 4. Perfil do Cliente em Risco

Com base nos fatores identificados, o perfil típico de cliente com maior risco de evasão é:

- Contrato **mensal**, sem compromisso de longo prazo
- Plano de **internet fibra óptica**
- Pagamento via **cheque eletrônico**
- **Pouco tempo** de contrato (primeiros meses)
- **Sem serviços adicionais** contratados (suporte técnico, segurança online)
- **Fatura digital** ativada

---

## 5. Estratégias de Retenção

### 5.1 Converter contratos mensais para anuais ou bienais

Essa é a ação com maior potencial de impacto. Oferecer benefícios concretos para migração — desconto progressivo, meses gratuitos, upgrades de plano — reduz diretamente o risco de evasão ao criar um compromisso formal com o cliente.

### 5.2 Programa de atenção especial nos primeiros meses

Clientes novos são os mais vulneráveis. Um programa de onboarding estruturado — contato proativo, tutoriais, suporte dedicado nos primeiros 3 a 6 meses — pode aumentar significativamente a retenção nesse período crítico.

### 5.3 Investigar a experiência dos clientes de fibra óptica

O fato de fibra óptica ser fator de risco merece atenção. Pesquisas de satisfação segmentadas para esse grupo podem revelar problemas específicos de qualidade, atendimento ou expectativa que não estão sendo endereçados.

### 5.4 Incentivar a adoção de serviços adicionais

Clientes com suporte técnico e segurança online contratados cancelam menos. Oferecer esses serviços em trial gratuito ou com desconto no pacote pode aumentar o engajamento e criar dependência positiva do ecossistema da empresa.

### 5.5 Migrar clientes do cheque eletrônico para débito automático ou cartão

O método de pagamento é um proxy de engajamento. Facilitar a migração para formas de pagamento automáticas reduz o atrito mensal e pode diminuir o churn passivo — aquele causado simplesmente pela fricção do processo de pagamento.

---

## 6. Conclusão

Os dois modelos treinados convergem em um diagnóstico claro: **a evasão de clientes está fortemente ligada à falta de vínculo de longo prazo com a empresa**. Contratos mensais, ausência de serviços adicionais e pouco tempo de relacionamento são os principais sinais de alerta.

A boa notícia é que todos esses fatores são acionáveis — a empresa tem instrumentos diretos para intervir em cada um deles. Com o modelo preditivo em produção, é possível identificar proativamente os clientes em risco e acionar as estratégias de retenção antes que o cancelamento aconteça, transformando um problema reativo em uma vantagem competitiva.
