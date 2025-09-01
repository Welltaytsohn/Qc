# 📊 Dashboard:
https://app.powerbi.com/view?r=eyJrIjoiZGM5ODEwZGQtNzViNi00Y2QzLWJiOGMtNzA0YWJjNGE3M2Q2IiwidCI6ImIyZTE2Mjk3LTJlZDYtNDFiOC1iODIyLWE5NTRlOTViZDJmMCIsImMiOjR9



# 📱 Análise de Apps da Google Play Store

Este projeto realiza uma **análise exploratória e preditiva** dos dados da Google Play Store e suas reviews, 
com foco em responder perguntas de negócio como:

- Quais **apps ou categorias** têm maior potencial de crescimento?
- Como está a **percepção geral dos usuários**?
- Quais **fatores influenciam a aceitação** de um app?

---

## 📂 Fontes de Dados

- **[Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps)**
- **[Google Play Store Reviews](https://www.kaggle.com/datasets/prakharrathi25/google-play-store-reviews)**

Ambos os datasets estão disponíveis no Kaggle.

---

## 🛠️ Pipeline de Análise

1. **Carregamento dos dados**
   - Datasets baixados do Kaggle.
   - Leitura com Pandas e Spark (Databricks).

2. **Limpeza e padronização**
   - Normalização de colunas (`Installs`, `Size`, `Genres`, `Android Ver`, `Current Ver`).
   - Criação de variáveis categóricas como `instalacoes_cat`, `tamanho_app_cat`, `genero_cat`.

3. **Enriquecimento com reviews**
   - Junção (`INNER JOIN`) de `df` (apps) com `df_reviews` (reviews).
   - Cálculo de métricas de sentimento, polaridade e subjetividade.

4. **Criação do DataFrame `app_metrics`**
   - Integra metadados + métricas de aceitação + score de crescimento.
   - Este é o **dataframe final**, usado tanto para análise quanto para exportação ao Power BI.

---

## 📊 Perguntas Respondidas

1. **Quais apps ou categorias têm maior potencial de crescimento?**
   - Métricas: `growth_potential_score`, `pct_pos`, `avaliacao_media`, `total_avaliacoes`.

2. **Como está a percepção dos usuários?**
   - Distribuição de sentimentos (Positive / Negative / Neutral).
   - Polaridade e subjetividade médias.

3. **Quais fatores influenciam a aceitação?**
   - Cruzamento por `categoria_app`, `tamanho_app_cat`, `Faixa_Preco`, `tipo`, etc.
  
## 📐 Métrica Principal: Growth Potential Score

Para identificar os apps com maior **potencial de crescimento**, foi criada a métrica **`growth_potential_score`**.  
Ela combina três dimensões importantes:

1. **Aceitação dos usuários**  
   - Percentual de reviews positivos (`pct_pos`).  
   - Normalizado de 0 a 1 para dar comparabilidade entre apps.

2. **Qualidade percebida**  
   - Nota média do app (`avaliacao_media`, variando de 1 a 5).  
   - Reescalada para o intervalo [0,1], onde 1 representa avaliação máxima.

3. **Relevância/Tração atual**  
   - Volume total de avaliações (`total_avaliacoes`).  
   - Aplicado log10 para reduzir distorção entre apps muito grandes e pequenos.

---

### 🧮 Fórmula

growth_potential_score = 
   (0.50 * pct_pos_norm) +
   (0.30 * rating_norm) +
   (0.20 * log_reviews_norm)


---

## ⚡ Tecnologias Usadas

- **Python** → pandas, numpy, matplotlib, plotly
- **PySpark / Databricks** → queries SQL em DataFrames
- **Power BI** → dashboards interativos
