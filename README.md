Análise Exploratória do Crédito Rural Brasileiro – 2026
Integrantes
Carolina Vasconcelos
Cleisson
Daniel
Objetivo
Realizar uma análise exploratória dos dados de crédito rural no Brasil utilizando Python, Pandas, NumPy, Matplotlib e Git.

Base de Dados
Arquivo utilizado:

MATRIZ_CR_TIPO_PESSOA_2026.csv

A base contém informações sobre operações de crédito rural realizadas no Brasil em 2026.

Devido ao tamanho do arquivo (aproximadamente 77 MB), ele não foi armazenado diretamente no repositório.

Perguntas da Análise
Qual perfil de beneficiário concentra maior quantidade de operações?
Como as operações de crédito rural estão distribuídas entre as regiões brasileiras?
Existe diferença entre os gêneros?
Como as operações se distribuem entre as diferentes faixas etárias?
Quais regiões apresentam maior concentração de operações?
Ferramentas Utilizadas
Python
Pandas
NumPy
Matplotlib
Seaborn
Jupyter Notebook
Git
GitHub
VS Code
Diagnóstico de Qualidade dos Dados
Foram realizadas verificações iniciais para avaliar a qualidade da base de dados.

Resultados
Total de registros: 189.907
Total de colunas: 28
Valores nulos: não identificados nas colunas analisadas
Registros duplicados: 0
Análises Realizadas
Distribuição por Gênero
Foi realizada uma análise da distribuição das operações por gênero dos beneficiários.

Distribuição por Região
As regiões Sul e Sudeste apresentaram maior concentração de operações de crédito rural.

Distribuição por Faixa Etária
Foi analisada a frequência das operações por faixa etária dos beneficiários.

GroupBy
Foi utilizada a função groupby() para consolidar e comparar informações por região.

Pivot Table
Foi criada uma tabela dinâmica para analisar simultaneamente região e gênero.

Uso de NumPy
Foi aplicada uma normalização dos valores por região utilizando NumPy.

Resultado da normalização:

Valor mínimo: 0.0
Valor máximo: 1.0
Principais Resultados
A região Sul apresentou a maior concentração de operações.
A região Norte apresentou a menor concentração de operações.
Não foram encontrados registros duplicados.
Não foram identificados valores nulos nas colunas analisadas.
A normalização utilizando NumPy foi realizada com sucesso.
Estrutura do Projeto
projeto/

├── README.md

├── dados/

│ └── link.txt

├── notebooks/

│ └── analise.ipynb

└── .gitignore

Como Executar
Instale as dependências:

pip install pandas numpy matplotlib seaborn jupyter
Abra o notebook:

jupyter notebook
Execute o arquivo:

notebooks/analise.ipynb
Conclusão
A análise exploratória permitiu identificar padrões relevantes na distribuição do crédito rural brasileiro em 2026.

Os resultados demonstraram diferenças importantes entre regiões, gêneros e faixas etárias, além de evidenciar a concentração das operações em determinadas regiões do país.

O projeto permitiu aplicar conceitos de limpeza, transformação, visualização e análise de dados utilizando Python, Pandas e NumPy.
