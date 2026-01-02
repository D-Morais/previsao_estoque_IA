# 🧠 Previsão Inteligente de Estoque  
Desafio de Ciência de Dados e Machine Learning

Este projeto tem como objetivo desenvolver um modelo preditivo capaz de realizar **previsão de estoque** e **previsão de consumo (saída de estoque)** utilizando apenas as seguintes variáveis fornecidas no dataset:

- **ID_PRODUTO**
- **DATA_EVENTO**
- **PRECO**
- **FLAG_PROMOCAO**
- **QUANTIDADE_ESTOQUE**

O desafio envolve a criação de modelos de Machine Learning que aprendam com o histórico de estoque, preço e promoções, estimando tanto **o nível de estoque futuro** quanto **o consumo previsto do próximo período**.

---

## 🚀 Objetivos do Projeto

### ✔ Prever a **Quantidade de Estoque Futuro**  
O modelo estima o estoque do próximo período (ex.: dia seguinte), considerando efeitos de preço, promoções e padrões históricos.

### ✔ Prever o **Consumo / Saída de Estoque**  
A partir da variação de estoque ao longo do tempo, o modelo reconstrói a quantidade consumida e prevê a demanda futura.

Essas previsões apoiam decisões como:

- reposição de estoque  
- identificação de produtos com risco de ruptura  
- efeitos de promoções e mudanças de preço  
- análise de sazonalidade  

---

## 📂 Estrutura do Dataset

| Coluna            | Descrição |
|-------------------|-----------|
| **ID_PRODUTO**       | Identificador único do produto |
| **DATA_EVENTO**      | Data do registro |
| **PRECO**            | Preço do produto no dia |
| **FLAG_PROMOCAO**    | Indica se o item estava em promoção (0/1) |
| **QUANTIDADE_ESTOQUE** | Quantidade de estoque disponível no período |

---

# 🔧 Metodologia

A solução foi implementada em Python seguindo as melhores práticas de Ciência de Dados e séries temporais.

---

## 🏗 1. Preparação dos Dados

- Conversão da coluna DATA_EVENTO para datetime  
- Ordenação por produto e data  
- Criação de features derivadas:

### 📅 **Features de data**
- ano  
- mês  
- dia  
- dia da semana  
- sazonalidade indireta  

### 📉 **Features de estoque**
- estoque do dia anterior (lag 1)  
- estoque da semana anterior (lag 7)  
- variação de estoque  
- média móvel de 7 dias  

### 💸 **Features comerciais**
- preço do dia anterior  
- diferença de preço  
- indicador de promoção  

---

## 📊 2. Reconstrução do Consumo (quando necessário)

Como o dataset não inclui vendas diretamente, o consumo é reconstruído via:



consumo = estoque_hoje - estoque_amanha


Consumos negativos representam reposição e são tratados adequadamente.

---

## 🤖 3. Algoritmos Utilizados

Para ambos os problemas (estoque futuro e consumo), o modelo utilizado foi:

### **XGBoost Regressor**
- excelente desempenho em séries temporais com múltiplas variáveis  
- captura efeitos não-lineares  
- interpreta bem impactos de promoção e preço   
- robusto contra ruídos e outliers  

---

## 📈 4. Avaliação

O conjunto de dados foi dividido em:

- **Treino:** 80%  
- **Teste:** 20% (mantendo ordem temporal)

A métrica escolhida foi:

- **MAE — Mean Absolute Error**

---
