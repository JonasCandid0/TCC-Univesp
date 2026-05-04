# Análise Espacial e Temporal de Encalhes de Fauna Marinha no Litoral de São Paulo

Este repositório contém o código do Trabalho de Conclusão de Curso (TCC) desenvolvido para o Bacharelado em Ciência de Dados da UNIVESP. O projeto utiliza dados públicos do **Sistema de Informação de Monitoramento da Biota Aquática (SIMBA)** para analisar padrões espaciais e temporais de encalhes de fauna marinha no litoral paulista, aplicando técnicas de ciência de dados e geoprocessamento em Python.

---

## Objetivo do Projeto

Identificar quais municípios do litoral paulista apresentam maior taxa de encalhes por esforço de monitoramento e verificar se existe variação sazonal na frequência mensal de encalhes, considerando a proporção de animais encontrados mortos por classe taxonômica.

**Objetivos específicos:**
- Mapear a distribuição geográfica dos encalhes no litoral de SP
- Analisar a evolução temporal e sazonalidade dos encalhes
- Avaliar a proporção de animais vivos e mortos por classe taxonômica
- Normalizar os encalhes pelo esforço de monitoramento para identificar hotspots reais
- Produzir mapas estáticos e interativos para comunicação dos resultados

---

## Datasets utilizados (SIMBA)

| Dataset | Registros | Descrição |
|---|---|---|
| Ocorrências de Fauna Alvo | 34.658 | Registro individual de cada encalhe |
| Biometrias | 31.440 | Medidas biométricas dos animais |
| Esforços de Monitoramento | 428.371 | Registros de saídas de monitoramento por praia |

---

## Estrutura do Notebook

### Fase 1 — Tratamento Inicial
Leitura e filtragem dos 3 datasets do SIMBA. Seleção das colunas relevantes, conversão de tipos (datas para `datetime`, variáveis categóricas para `category`) e merge entre Ocorrências e Biometrias via `pd.merge()` com `how='left'`, gerando o `df_master` com 34.658 registros.

### Fase 2 — Relacionamento e Higienização
Cruzamento das tabelas de Ocorrências com Biometrias pelas chaves `Identificador da ocorrência` e `Identificador do indivíduo`. Verificação de integridade com auditoria de linhas antes e depois do merge.

### Fase 3 — Análise Exploratória e Séries Temporais
- **Série mensal:** evolução dos encalhes mês a mês ao longo dos anos
- **Sazonalidade:** total de encalhes por mês do ano (Jan–Dez) para identificar padrões cíclicos
- **Encalhes por classe:** ranking dos grupos taxonômicos mais afetados
- **Condição dos animais:** proporção de vivos vs mortos
- **Taxa normalizada:** encalhes divididos pelo esforço de monitoramento por praia, eliminando o viés de praias mais monitoradas

### Fase 4 — Geoprocessamento e Análise Espacial
- Correção das coordenadas exportadas com erro pelo SIMBA (dois pontos em vez de um)
- Criação de GeoDataFrame de pontos (`gdf_encalhes`) e de linhas (`gdf_esforcos`)
- Mapa estático de distribuição dos encalhes por classe sobre o shapefile do estado de SP
- Mapa de densidade de encalhes por município
- Ranking dos 15 municípios com maior número de encalhes

---

## Ferramentas Utilizadas

- **Linguagem:** Python 3.10+
- **Ambiente:** Google Colab
- **Bibliotecas:**
  - `pandas` — manipulação e análise de dados
  - `numpy` — operações numéricas
  - `geopandas` — análise espacial e criação de GeoDataFrames
  - `shapely` — criação de geometrias (Point, LineString)
  - `matplotlib` — visualizações estáticas
  - `seaborn` — gráficos estatísticos

---

## Autores

Edson Mokiu Yabiku, Érica Catarino Marins, Gabriel Catarino Marins, Guilherme Almeida Ramos, Jonas Cândido Pereira, Marcelo Massayuki Hiray, Pedro Henrique Lapinha Flaminio

**Orientador:** Prof. Anderson Nogueira Cotrim  
**Instituição:** UNIVESP — Universidade Virtual do Estado de São Paulo  
**Curso:** Bacharelado em Ciência de Dados — 2026
