# 📉 Previsão de Evasão de Clientes (Churn)

Projeto desenvolvido como parte do **Challenge Alura** de Machine Learning. O objetivo é construir um pipeline preditivo capaz de identificar clientes com maior risco de cancelamento, gerando insights estratégicos para ações de retenção.

---

## 📋 Sobre o Projeto

A evasão de clientes (churn) é um dos principais desafios de empresas de serviços por assinatura. Antecipar quais clientes têm maior probabilidade de cancelar permite agir proativamente — antes que a perda aconteça.

Este projeto cobre todo o pipeline de Machine Learning, desde o pré-processamento dos dados até a interpretação dos resultados e elaboração de estratégias de retenção.

---

## 🗂️ Estrutura do Projeto

```
├── TelecomX_BR_pt2.ipynb        # Pipeline completo
├── dados_limpos_telecomx_br.csv # Dataset do challenge
├── relatorio_churn.md           # Relatório com insights e estratégias
└── README.md
```

---

## 🔄 Pipeline Desenvolvido

- **Pré-processamento** — remoção de colunas irrelevantes, encoding de variáveis categóricas (binárias e nominais) e normalização
- **Análise Exploratória** — distribuição de churn, boxplots, scatter plots e matriz de correlação
- **Modelagem** — treinamento de dois modelos com abordagens distintas
- **Avaliação** — métricas de classificação, matrizes de confusão e análise de overfitting/underfitting
- **Interpretação** — coeficientes da Regressão Logística e importância de variáveis do Random Forest

---

## 🤖 Modelos Utilizados

| Modelo | Normalização | Acurácia | Recall | F1-Score |
|---|---|---|---|---|
| Regressão Logística | ✅ StandardScaler | 75,0% | **79,9%** | **0,63** |
| Random Forest | ❌ | 79,9% | 50,0% | 0,57 |

A **Regressão Logística** foi o modelo recomendado para este contexto — Recall alto significa detectar mais clientes em risco, que é o objetivo central do negócio.

---

## 🔑 Principais Fatores de Evasão

Ambos os modelos convergiram nos mesmos fatores:

**Aumentam o risco de churn:**
- Contrato mensal (sem compromisso de longo prazo)
- Internet de fibra óptica
- Pagamento via cheque eletrônico
- Pouco tempo de contrato
- Ausência de serviços adicionais

**Reduzem o risco de churn:**
- Longo tempo de contrato
- Contrato bienal
- Suporte técnico e segurança online contratados

---

## 🛠️ Tecnologias

- Python 3
- Google Colab
- pandas
- scikit-learn
- matplotlib
- seaborn

---

## ▶️ Como Rodar o Projeto

O projeto roda inteiramente no **Google Colab** — não é necessário instalar nada localmente.

**1. Acesse o notebook**

Clique no badge abaixo para abrir diretamente no Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ElielSf/telecomx-br-pt2/blob/main/TelecomX_BR_pt2.ipynb)

Ou acesse manualmente em [colab.research.google.com](https://colab.research.google.com), clique em `Arquivo → Abrir notebook → GitHub` e cole a URL deste repositório.

**2. Execute todas as células em ordem**

No menu: `Ambiente de execução → Executar tudo`

---

## 📊 Dataset

Os dados utilizados são carregados diretamente do repositório — nenhum download manual é necessário. O notebook já contém a célula:

```python
df = pd.read_csv("https://raw.githubusercontent.com/ElielSf/telecomx-br-pt2/refs/heads/main/dados_limpos_telecomx_br.csv")
```

O dataset simula informações de clientes de uma empresa de telecomunicações, com variáveis como tipo de contrato, serviços contratados, tempo de relacionamento e método de pagamento.

| Variável | Descrição |
|---|---|
| `meses_contrato` | Tempo de contrato em meses |
| `contrato` | Tipo de contrato (mensal, anual, bienal) |
| `internet` | Tipo de serviço de internet |
| `cobranca_mensal` | Valor da mensalidade |
| `cobranca_total` | Total pago ao longo do contrato |
| `churn` | Se o cliente cancelou (1) ou não (0) |

---

## 👨‍💻 Autor

Desenvolvido como parte do **Challenge de Data Science — Alura** do programa **Oracle Next Education**.
