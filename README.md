Aqui está o arquivo **`README.md` completo e estruturado**, pronto para ser copiado e colado na raiz do repositório Git do seu projeto.

Ele cobre desde a apresentação do dataset oficial e das perguntas de negócio até o mapeamento detalhado da **adequação de 100% dos requisitos** da rubrica de avaliação.

---

```markdown
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

## 📊 O Dataset (`MATRIZ_CR_TIPO_PESSOA_2025.csv`)

* **Fonte:** Portal de Dados Abertos do Banco Central do Brasil (BCB) / SICOR.
* **Dimensões Analisadas:** 10.000 linhas de operações × 28 colunas de atributos.
* **Dicionário das Principais Variáveis:**

| Coluna | Tipo Original | Tipo Tratado | Descrição |
| --- | --- | --- | --- |
| `ANO_MES_EMISSAO` | `object` | `datetime64` | Data de emissão do contrato de crédito |
| `REGIAO` / `UF` | `object` | `category` | Localização geográfica da propriedade rural |
| `GENERO` | `object` | `category` | Gênero do titular (Masculino, Feminino, Não se aplica) |
| `BENEFICIARIO` | `object` | `category` | Enquadramento (PRONAF, PRONAMP, Demais Pessoas Físicas/Jurídicas) |
| `SEGMENTO_IF` / `NOME_IF` | `object` | `category` | Segmento e nome da Instituição Financeira concessora |
| `CUSTEIO_VALOR` | `object` | `float64` | Valor liberado para despesas de custeio agrícola/pecuário |
| `INVESTIMENTO_VALOR` | `object` | `float64` | Valor liberado para máquinas, infraestrutura e melhorias |
| `TOTAL_AREA` | `object` | `float64` | Área total financiada no contrato (hectares) |
| `TOTAL_QTDE` | `int64` | `int64` | Quantidade de contratos/operações associadas |
| `TOTAL_VALOR` | `object` | `float64` | Valor total consolidado do financiamento ($R\$$) |

---

## 🛠️ Adequação aos Requisitos do Projeto Final (Matriz de Rubrica)

Below is the complete compliance audit showing how each requirement was satisfied in the implementation:

### 1. Apresentação e Qualidade dos Dados (30%)

* [x] **Diagnóstico Inicial:** Levantamento de dimensões, uso de memória (2,14 MB) e mapeamento de tipos via `.info()` e `.isnull()`.
* [x] **Tratamento de Nulos e Inconsistências:** Conversão das colunas de texto no formato numérico brasileiro (`1639048,85`) para `float64`. Mapeamento categórico padronizado com `.map()`.
* [x] **Tratamento de Outliers por Subgrupo:** Cálculo do **Z-Score vetorizado por Região** com `NumPy`, garantindo que grandes operações agroindustriais no Centro-Oeste e Sudeste sejam avaliadas em seu grupo de comparação correto, sem distorcer o limite nacional.

### 2. Limpeza e Engenharia de Atributos (25%)

* [x] **Tratamento Seguro de Divisão por Zero:** Uso do `np.where` para cálculo condicional.
* [x] **Criação de 3 Colunas Derivadas:**
1. `VALOR_MEDIO_OPERACAO`: Ticket médio por contrato (`TOTAL_VALOR / TOTAL_QTDE`).
2. `VALOR_POR_HECTARE`: Densidade de crédito por área (`TOTAL_VALOR / TOTAL_AREA`).
3. `FAIXA_PORTE_CONTRATO`: Classificação por quantis via `pd.qcut` (*Pequeno Porte*, *Médio Porte*, *Grande Porte*, *Mega Operação*).



### 3. Uso de Pandas e NumPy (30%)

* [x] **Vetorização com NumPy:** Aplicação de `np.where` em lógicas condicionais e cálculo matricial do Z-Score regional ($Z = \frac{\vert{}X - \mu\vert{}}{\sigma}$).
* [x] **`groupby` Múltiplo:** Agregação por `['REGIAO', 'GENERO_PADRONIZADO']` calculando simultaneamente soma, média e mediana com `.agg()`.
* [x] **Combinação de Dados (`merge`):** Junção *left* com tabela auxiliar de domínio de perfis logísticos regionais, validada por `assert` de contagem de linhas.
* [x] **Tabela Dinâmica (`pivot_table`):** Cruzamento multidimensional entre `BENEFICIARIO` vs `REGIAO` para distribuição de recursos em R$ Milhões.
* [x] **4 Gráficos com Leitura em Texto:** Gráficos interativos/estáticos cobrindo Regiões, Gênero, Beneficiários e Segmento de Instituição Financeira, cada um acompanhado de análise explicativa.

### 4. Requisitos de Git (10%)

* [x] Repositório público com `README.md` detalhado.
* [x] Arquivo `.gitignore` configurado para ignorar `.ipynb_checkpoints`, `__pycache__` e ambientes virtuais.
* [x] Histórico de commits frequentes e descritivos (`feat:`, `refactor:`, `docs:`).
* [x] Uso de branches secundárias para desenvolvimento e *merge* na `main`.
* [x] Notebook commitado com **todas as células executadas e saídas visíveis em tela**.

---

## 💡 Principais Achados para Tomada de Decisão (15%)

1. **Concentração no Eixo Sul / Centro-Oeste:** O Sul (R$ 4,41 bilhões) e o Centro-Oeste (R$ 4,30 bilhões) absorvem 56,9% de todo o volume de crédito concedido no país, impulsionados pela alta mecanização e escala de safras.
2. **Disparidade no Crédito por Gênero:** Em operações para pessoas físicas, produtores masculinos captaram 80,4% dos recursos (R$ 8,36 bilhões), enquanto produtoras femininas acessaram apenas 19,6% (R$ 2,04 bilhões), apontando a necessidade de programas de fomento com equidade de gênero.
3. **Capilaridade do Cooperativismo:** As Cooperativas de Crédito e os Bancos Públicos são os principais agentes de distribuição do PRONAF e PRONAMP, demonstrando maior interiorização e presença física do que os bancos comerciais privados.

---

## ⚙️ Como Reproduzir a Análise

1. **Clonar o Repositório:**
```bash
git clone [https://github.com/seu-usuario/projeto-credito-rural-2025.git](https://github.com/seu-usuario/projeto-credito-rural-2025.git)
cd projeto-credito-rural-2025

```


2. **Instalar Dependências:**
```bash
pip install pandas numpy matplotlib seaborn jupyter

```


3. **Executar o Notebook:**
```bash
jupyter notebook notebooks/analise.ipynb

```



---

## 👨‍💻 Autores & Integrantes do Grupo

* **Carolina D. S. Vasconcelos**
* **Cleisson Nascimento**
* **Daniel Massita Tonolli**

```

```