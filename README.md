# 🌾 Análise Exploratória de Crédito Rural no Brasil (2025)
> **Projeto Final — DS-PY-004: Análise Exploratória de Dados com Python, NumPy, Pandas e Git**  
> **Instituição:** Ada Tech  
> **Base de Dados:** Matriz de Crédito Rural por Tipo de Pessoa (2025) — Banco Central do Brasil (BCB / SICOR)

---

## 📌 Visão Geral e Contexto de Negócio

O Crédito Rural é o principal instrumento de política agrícola no Brasil, financiando desde o pequeno produtor familiar até megagrupos agroindustriais. Esta análise investiga uma amostragem de **10.000 operações de financiamento concedidas em 2025**, extraídas diretamente dos microdados abertos do **Sistema de Concessão de Crédito Rural (SICOR)** do Banco Central do Brasil.

O objetivo principal do grupo é diagnosticar a qualidade dos dados brutos, realizar o tratamento e a engenharia de atributos e responder a perguntas estratégicas sobre a distribuição geográfica, inclusão de gênero e a atuação das instituições financeiras no campo.

---

## 🎯 Perguntas de Negócio (Definidas *a priori*)

1. **Concentração Regional:** Como se distribuem o volume financeiro total ($R\$$) e o ticket médio das operações entre as 5 regiões do Brasil?
2. **Inclusão Financeira de Gênero:** Qual é o nível de disparidade no acesso ao crédito rural individual entre produtores dos gêneros Masculino e Feminino?
3. **Efetividade dos Programas Sociais:** Qual é a participação dos programas de fomento (`PRONAF` para agricultura familiar e `PRONAMP` para médios produtores) em comparação com as operações de mercado dos Demais Produtores?
4. **Canais de Distribuição:** Qual o peso relativo das **Cooperativas de Crédito** versus **Bancos Públicos** no financiamento das atividades agropecuárias regionais?

---

## 🗂️ Estrutura do Repositório

```text
projeto-credito-rural-2025/
├── README.md                      <- Documentação principal do projeto
├── .gitignore                     <- Ignora checkpoints, caches e ambientes virtuais
├── dados/
│   └── MATRIZ_CR_TIPO_PESSOA_2025.csv <- Dataset público e bruto (10.000 linhas)
└── notebooks/
    └── analise.ipynb              <- Pipeline completo em Python com código e saídas executadas

```

---

# 📋 SUMÁRIO EXECUTIVO & AUDITORIA DE REQUISITOS DO PROJETO FINAL

**Curso:** DS-PY-004 — Análise Exploratória de Dados com Python, NumPy, Pandas e Git  
**Dataset Analisado:** Matriz de Crédito Rural 2025 (`MATRIZ_CR_TIPO_PESSOA_2025.csv` — Banco Central do Brasil / SICOR)  
**Amostra Avaliada:** 10.000 operações de financiamento agropecuário (2025)

---

## 📌 1. Apresentação da Base e Perguntas de Negócio (Requisito: 10%)

### Q1.1: De onde vieram os dados e qual o recorte temporal?
> **Resposta:** Os dados derivam dos microdados públicos abertos do Sistema de Concessão de Crédito Rural (SICOR) gerido pelo Banco Central do Brasil (BCB), cobrindo as emissões de contratos do ano-exercício de 2025.

### Q1.2: Qual o tamanho da base e o significado das variáveis?
> **Resposta:** A amostra contém 10.000 registros e 28 colunas originais, cobrindo aspectos espaciais (Região, UF), demográficos (Gênero, Faixa Etária, Tipo de Pessoa), financeiros/operacionais (Áreas, Quantidades e Valores para Custeio, Investimento, Comercialização e Industrialização) e institucionais (Programa, Subprograma, Fonte de Recurso, Instituição Financeira).

### Q1.3: Quais foram as 4 Perguntas de Negócio definidas *a priori*?
> **Resposta:**
> 1. **Concentração Regional:** Como se distribui o volume total de crédito (R$) e o ticket médio entre as 5 regiões brasileiras?
> 2. **Inclusão Financeira de Gênero:** Qual a discrepância de acesso a recursos financeiros entre homens e mulheres no meio rural?
> 3. **Efetividade dos Programas Sociais:** Qual o papel relativo do PRONAF e PRONAMP em relação às operações de mercado dos demais produtores?
> 4. **Atuação do Sistema Financeiro:** Qual o peso relativo das Cooperativas de Crédito versus Bancos Públicos na operacionalização dos recursos?

---

## 🔍 2. Diagnóstico de Qualidade (Requisito: 20%)

### Q2.1: Qual o diagnóstico estrutural e uso de memória da base bruta?
> **Resposta:** A amostra bruta ocupa **2,14 MB** de memória RAM. As colunas numéricas financeiras estavam originalmente serializadas em formato texto padrão brasileiro (ex: `"1639048,85"`), exigindo *parsing* para `float64`.

### Q2.2: Qual a presença de valores nulos e duplicados?
> **Resposta:** 0 linhas duplicadas e 0 nulos nas colunas principais, porém com presença da categoria categórica `'NÃO SE APLICA'` no campo `GENERO` (referente a contratos de Pessoas Jurídicas), tratada via mapeamento padronizado (`.map()`).

### Q2.3: Como foi feita a detecção e avaliação de outliers?
> **Resposta:** A avaliação de outliers **não foi realizada na coluna inteira**, mas sim no **grupo de comparação correto (Região)**. Foi calculado o Z-Score vetorizado por região com NumPy. Foram identificados 68 contratos com Z > 3, correspondendo a grandes operações de agroindústrias e cooperativas em São Paulo e Mato Grosso, mantidos na análise por representarem a realidade do grande agronegócio nacional.

---

## 🛠️ 3. Limpeza e Transformação (Requisito: 25%)

### Q3.1: Quais foram as principais decisões de tratamento e suas justificativas?
> **Resposta:**
> - **Sintaxe Numérica:** Conversão de strings com vírgula e ponto para `float64` para possibilitar cálculos matemáticos.
> - **Padronização:** Mapeamento de rótulos categóricos (`GENERO`) via `.map()`.
> - **Tratamento de Divisão por Zero:** Uso do `np.where` ao calcular razões de ticket médio e valor por hectare.

### Q3.2: Quais foram as 3 colunas derivadas criadas?
> **Resposta:**
> 1. **`VALOR_MEDIO_OPERACAO`:** Relação `TOTAL_VALOR / TOTAL_QTDE` calculada via `np.where`.
> 2. **`VALOR_POR_HECTARE`:** Densidade financeira do contrato (`TOTAL_VALOR / TOTAL_AREA`).
> 3. **`FAIXA_PORTE_CONTRATO`:** Discretização em 4 quantis por `pd.qcut` (*Pequeno Porte*, *Médio Porte*, *Grande Porte*, *Mega Operação*).

---

## 📊 4. Análise Exploratória e Operações Pandas/NumPy (Requisito: 30%)

### Q4.1: Onde e por que o NumPy foi utilizado de forma vetorizada?
> **Resposta:** O NumPy foi utilizado na construção de regras condicionais vetorizadas (`np.where`) e na fórmula estatística do Z-Score regional:
>
> $$Z = \frac{\vert{}X - \mu\vert{}}{\sigma}$$
>
> garantindo alta performance computacional sem a necessidade de laços `for`.

### Q4.

___

