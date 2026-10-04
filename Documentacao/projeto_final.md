# Projeto Final — DS-PY-004
## Análise exploratória de dados com Python, NumPy, Pandas e Git

**Formato:** grupos de 3 a 4 pessoas
**Entregável:** repositório público no GitHub + apresentação de 10 minutos

---

## O desafio

O grupo vai assumir o papel de uma equipe de dados que recebeu uma base **real e crua** e precisa responder: *o que esses dados têm a dizer?*

Não existe resposta certa pré-definida. O que se avalia é o **processo**: como vocês diagnosticaram, trataram e interrogaram os dados, e se as conclusões apresentadas se sustentam nos números que vocês mesmos produziram.

## Escolha da base

Escolham **uma** base pública, com no mínimo **1.000 linhas** e **8 colunas**, sendo pelo menos 3 numéricas e 2 categóricas. Sugestões de fontes:

- [Portal Brasileiro de Dados Abertos](https://dados.gov.br)
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [IBGE — SIDRA](https://sidra.ibge.gov.br)
- [Base dos Dados](https://basedosdados.org)
- Dados do TSE, INEP, ANAC, ANS, Portal da Transparência

> A base deve ser **suja de verdade**. Bases já tratadas de exercício (Iris, Titanic) não serão aceitas — o trabalho de limpeza é o coração do projeto.


---

## O que precisa estar no repositório

```
seu-projeto/
├── README.md              <- explica o projeto, a base e como reproduzir
├── notebooks/
│   └── analise.ipynb      <- a análise, do início ao fim
├── dados/
│   └── (ou o link para a base, se for grande demais para o Git)
└── .gitignore
```

### 1. Apresentação da base e das perguntas (10%)
- De onde vieram os dados, o que cada coluna significa, qual o recorte temporal
- **3 a 5 perguntas** que vocês querem responder, definidas **antes** da análise

### 2. Diagnóstico de qualidade (20%)
- Dimensões, tipos, uso de memória
- Faltantes por coluna (quantidade e percentual)
- Duplicados, categorias inconsistentes, valores inválidos
- Identificação de outliers com método justificado (IQR ou z-score), avaliados no **grupo de comparação correto**

### 3. Limpeza e transformação (25%)
- Cada decisão de tratamento **justificada em texto**: por que imputar em vez de remover? por que a mediana do grupo e não a média geral?
- Ao menos: tratamento de faltantes, remoção/consolidação de duplicados, padronização de categorias, criação de pelo menos 3 colunas derivadas
- Uso de `map`, `apply`, `np.where`/`np.select`, `cut`/`qcut` onde fizer sentido

### 4. Análise exploratória (30%)
- Respostas às perguntas definidas no item 1, com evidência numérica
- Uso obrigatório de: `groupby` com agregação múltipla, ao menos um `merge` (pode ser com uma tabela auxiliar que vocês montarem) e ao menos uma `pivot_table`
- Ao menos 4 gráficos, cada um acompanhado de uma leitura em texto (o gráfico sozinho não conta)
- Uso de NumPy em pelo menos um cálculo relevante (normalização, z-score, operação matricial, simulação)

### 5. Conclusões (15%)
- 3 a 5 achados defensáveis, escritos para uma **área de negócio**, não para outro programador
- Limitações da análise: o que os dados **não** permitem afirmar
- Próximos passos: o que vocês investigariam com mais tempo ou mais dados

---

## Requisitos de Git

Não é um detalhe — vale nota:

- [ ] Repositório público, com README preenchido
- [ ] **Todos** os integrantes com commits (o histórico mostra quem fez o quê)
- [ ] No mínimo 15 commits, com mensagens descritivas (`feat: adiciona tratamento de outliers`, não `update`)
- [ ] Uso de pelo menos uma branch além da `main`
- [ ] `.gitignore` adequado (nada de `.ipynb_checkpoints`, `__pycache__` ou credenciais)
- [ ] Notebook commitado **com as saídas executadas**

---

## A apresentação (aula 7)

**10 minutos + 2 de perguntas.** Sugestão de divisão:

| Tempo | Conteúdo |
|---|---|
| 1 min | A base e por que ela foi escolhida |
| 2 min | Estado inicial: o que estava errado nos dados |
| 2 min | Principais decisões de tratamento e suas justificativas |
| 4 min | Os achados, com os gráficos |
| 1 min | Limitações e próximos passos |

Apresentem a partir do notebook ou de slides — o que preferirem. Todos os integrantes devem falar.

---

## Critérios de avaliação por rubrica

| Eixo | Em desenvolvimento | Desenvolvido | Referência |
|---|---|---|---|
| **Git** | Commits concentrados em uma pessoa ou mensagens genéricas | Histórico distribuído, mensagens claras, `.gitignore` correto | Uso fluente de branches; README que permite outra pessoa reproduzir a análise |
| **NumPy** | Uso apenas incidental | Aplica vetorização em pelo menos um cálculo relevante | Escolhe NumPy conscientemente por eficiência e explica o porquê |
| **Pandas** | Operações básicas com erros de alinhamento ou perda silenciosa de linhas | Domina `groupby`, `merge` e `pivot` e confere o resultado | Encadeia operações de forma legível e verifica integridade a cada etapa |
| **Leitura e gravação** | Só lê csv simples | Lida com configurações não triviais e grava em formato adequado | Justifica a escolha do formato de saída (ex.: parquet por tipos e tamanho) |
| **Limpeza e transformação** | Apaga o que incomoda, sem justificar | Trata faltantes, duplicados e outliers justificando cada decisão | Compara estratégias alternativas e mede o impacto de cada uma antes de decidir |
| **Comunicação** | Apresenta código, não conclusões | Achados claros, apoiados em números | Narrativa que uma área de negócio entenderia e usaria para decidir |

---

## Erros que mais custam nota

1. Concluir coisas que os dados não sustentam (correlação apresentada como causa).
2. Apagar linhas com faltantes sem verificar quantas e quais são — e sem dizer nada sobre isso.
3. Tratar como outlier tudo que é extremo na coluna inteira, sem olhar o grupo de comparação.
4. Fazer `merge` e não conferir se o número de linhas mudou.
5. Gráfico sem título, sem eixo nomeado e sem uma frase dizendo o que ele mostra.
6. Repositório com um único commit no dia da entrega.
