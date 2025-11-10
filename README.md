#  Modelo de Classificação de Citações — SBIE (2001–2024)

Este projeto tem como objetivo **analisar e classificar publicações do Simpósio Brasileiro de Informática na Educação (SBIE)** entre os anos de 2001 e 2024, com base em seus **resumos, títulos e instituições de autoria**, buscando identificar padrões entre **artigos mais e menos citados**.

O notebook e script realizam um fluxo completo de **pré-processamento, tradução, engenharia de atributos, análise exploratória e modelagem com SVM (Support Vector Machine)** e ajuste de hiperparâmetros.

---

##  Roteiro do Pipeline

> **Dados crus → Limpeza inicial + Feature Engineering → EDA → Modelagem**

---

##  Estrutura do Projeto

```text
modelo_classificação_citações.py
├── Carregamento dos dados
├── Limpeza inicial e tratamento de valores nulos
├── Extração e mapeamento de afiliações institucionais (via API OpenAlex)
├── Tradução automática de resumos e títulos (GoogleTranslator)
├── Vetorização do texto com TF-IDF
├── Balanceamento das classes de citação
├── Análise exploratória de dados (EDA)
│   ├── Gráficos de citações por ano
│   ├── Universidades mais frequentes
│   ├── Palavras mais representativas
├── Modelagem
│   ├── Treinamento com SVM (RBF kernel)
│   ├── Avaliação com acurácia
└── Exportação do dataset final (`df_final.csv`)
```

#  Requisitos

##  Bibliotecas principais

* pandas
* numpy
* matplotlib
* seaborn
* scikit-learn
* deep-translator
* tqdm
* requests
* ast

##  Instalação

```
pip install pandas numpy matplotlib seaborn scikit-learn deep-translator tqdm requests
```

##  Descrição dos dados


Cada registro representa um artigo publicado no SBIE, contendo:

* titulo — Título do artigo
* resumo — Resumo do artigo
* citacoes — Número de citações (fonte: OpenAlex ou similar)
* afiliacoes — Lista de instituições associadas aos autores
* ano — Ano de publicação

#  Etapas do Processamento
## 1. Limpeza de dados

* Remoção de registros sem resumo.
 
* Exclusão de entradas de capa, contra-capa e editoriais.

* Preenchimento de valores nulos em citacoes.

## 2. Engenharia de Atributos

* Extração dos IDs institucionais via API OpenAlex.

* Criação de colunas binárias para presença de cada instituição.

* Tradução de textos do português para o inglês.

* Vetorização textual com TF-IDF (1000 features).

## 3. Balanceamento de classes

* A classe-alvo (citacoes) foi binarizada pela mediana.

* Amostras da classe majoritária foram removidas para balanceamento.

## 4. EDA (Análise Exploratória de Dados)

* Distribuição de citações por ano.

* Instituições mais frequentes entre artigos citados.

* Palavras mais relevantes nos resumos.

## 5. Modelagem

* Divisão em treino (70%) e teste (30%).

* Modelo: SVM 

Avaliação: Acurácia.
69.66%

## 6. Ajustes nos Hiperparâmetros

* SVM: C, gamma, kernel
* RandomForest: n_estimators, max_depth, min_samples_leaf
* MLP: hidden_layers_size, activation, solver
* Decision Tree: max_depth, min_samples_split, criterion
