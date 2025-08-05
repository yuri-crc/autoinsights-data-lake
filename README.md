# autoinsights-data-lake
Construção de um Data Lake automotivo com Databricks, PySpark e dados públicos (recall, FIPE, consumo veicular). Pipeline completo com ingestão, tratamento e visualização em Power BI.


# 🚗 AutoInsights – Data Lake Automotivo

Projeto de Engenharia de Dados para analisar dados públicos relacionados ao setor automotivo no Brasil.

## 📊 Objetivo

Construir um Data Lake com arquitetura em camadas (Bronze, Silver, Gold) utilizando **Databricks Community + PySpark**, para coletar, tratar e analisar dados de:

- Recalls de veículos (dados.gov.br)
- Preços médios da Tabela FIPE
- Consumo energético de veículos (INMETRO)

---

## 🔧 Tecnologias

- Python (pandas, requests)
- Databricks Community (PySpark + Delta Lake)
- Power BI (dashboard final)
- Git/GitHub

---

## 📐 Arquitetura


┌─────────────────────────┐
│       Fontes de Dados    │
├─────────────────────────┤
│ Recall - Governo Federal │
│ FIPE API                 │
│ INMETRO PBE Veicular     │
│ (Opcional) OLX/Webmotors │
└─────────────┬───────────┘
              │
              ▼

      ┌────────────────┐
      │  Ingestão       │
      │ (Python/NiFi)   │
      │  - requests     │
      │  - pandas       │
      └───────┬────────┘
              │ Dados brutos (raw)
              ▼
      
      ┌────────────────────────┐
      │ Camada Bronze (Delta)  │
      │  - CSV/Parquet         │
      │  - Estrutura original  │
      └─────────┬─────────────┘
                │ Limpeza e padronização (Spark)
                ▼
      
      ┌────────────────────────┐
      │ Camada Silver (Delta)  │
      │  - Tipos corrigidos    │
      │  - Datas formatadas    │
      │  - Dados sem nulos     │
      └─────────┬─────────────┘
                │ Agregações e análises
                ▼
      ┌────────────────────────┐
      │ Camada Gold (Delta)    │
      │  - Ranking recalls     │
      │  - Preço médio FIPE    │
      │  - Consumo médio       │
      │  - Tabelas p/ BI       │
      └─────────┬─────────────┘
                │
                ▼
      ┌────────────────────────┐
      │ Visualização (Power BI)│
      │  - Dashboard interativo│
      │  - Mapa de calor       │
      │  - Tendências          │
      └────────────────────────┘


---

## 📁 Estrutura
data/
├── raw/ # Dados brutos
├── processed/ # Dados tratados
└── gold/ # Agregações para análise

notebooks/
├── 01_ingestion_recall.ipynb
├── 02_clean_transform.ipynb
└── 03_analysis_powerbi.ipynb


## 📈 Resultados Esperados

- Ranking de veículos com mais recalls
- Comparativo de consumo por tipo de combustível
- Evolução de preços FIPE
