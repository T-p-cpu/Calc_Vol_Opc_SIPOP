Projeto de Cálculo de Volatilidades e Precificação de Opções sobre o PLD
Autor: Prof. Paulo Cavalcante  
Versão: 2026
---
PARTE 1 — Cálculo de Volatilidades Condicionais Estocásticas com Base na Volatilidade Diária do PLD
1. Descrição Geral
A Parte 1 do projeto tem como objetivo estimar a volatilidade condicional do Preço de Liquidação das Diferenças (PLD) para o Submercado Sudeste do Sistema Interligado Nacional (SIN).
A estimação é realizada a partir das volatilidades diárias realizadas do PLD, utilizando cinco modelos de volatilidade:
HAR-RV
EGARCH
GJR-GARCH
EGARCH-t
GJR-GARCH-t
A arquitetura foi organizada em cinco códigos Python independentes, sendo um para cada modelo de volatilidade.
Cada modelo gera, conforme sua especificação:
volatilidade realizada do PLD;
volatilidade diária estimada pelo modelo;
volatilidade semanal;
volatilidade mensal;
volatilidade anual;
volatilidades anualizadas correspondentes aos horizontes considerados.
---
2. Modelos de Volatilidade
Os cinco modelos utilizados são:
Nº	Modelo	Descrição
1	HAR-RV	Heterogeneous Autoregressive Realized Volatility
2	EGARCH	Exponential GARCH com distribuição Normal
3	GJR-GARCH	GJR-GARCH com distribuição Normal
4	EGARCH-t	Exponential GARCH com distribuição Student-t
5	GJR-GARCH-t	GJR-GARCH com distribuição Student-t
---
3. Requisitos de Pacotes Python
Instale as dependências necessárias antes de executar os notebooks.
```bash
pip install pandas numpy scipy arch openpyxl matplotlib seaborn plotly xlsxwriter python-docx docx2pdf
```
> **Observação:** `math`, `os`, `warnings` e `datetime` fazem parte da biblioteca padrão do Python e, portanto, **não devem ser instalados via `pip`**.
Para conversão automática dos relatórios DOCX para PDF:
```bash
pip install docx2pdf
```
A utilização do `docx2pdf` é recomendada principalmente em ambiente Windows com Microsoft Word disponível.
---
4. Estrutura de Pastas
```text
1-CALCULO_VOLATILIDADES/
│
├── EGARCH/
│   ├── CÁLCULO_VOLATILIDADE_EGARCH.ipynb
│   ├── PLD_volatilidades_EGARCH
│   └── PREÇO MED DIARIO PLD VERTICAL PERIODO 17-04-18 A 03-06-25
│
├── EGARCH-t/
│   ├── CÁLCULO VOLATILIDADE_EGARCH-t
│   ├── Volatilidades_EGARCH_t_1W1M1Y
│   └── PREÇO MED DIARIO PLD VERTICAL PERIODO 17-04-18 A 03-06-25
│
├── GJR/
│   ├── CÁLCULO_VOLATILIDADE_GJR.ipynb
│   ├── PLD_volatilidades_GJR
│   └── PREÇO MED DIARIO PLD VERTICAL PERIODO 17-04-18 A 03-06-25
│
├── GJR-t/
│   ├── CÁLCULO_VOLATILIDADE_GJR_t.ipynb
│   ├── PLD_volatilidades_GJR-t
│   └── PREÇO MED DIARIO PLD VERTICAL PERIODO 17-04-18 A 03-06-25
│
└── HAR-RV/
    ├── CÁLCULO_VOLATILIDADE_HAR_RV.ipynb
    ├── PLD_volatilidades_HAR-RV
    └── PREÇO MED DIARIO PLD VERTICAL PERIODO 17-04-18 A 03-06-25
```
---
5. Execução dos Códigos
5.1 EGARCH
Notebook:
```text
CÁLCULO_VOLATILIDADE_EGARCH.ipynb
```
Saída:
```text
PLD_volatilidades_EGARCHC.xlsx
```
---
5.2 EGARCH-t
Notebook:
```text
CÁLCULO VOLATILIDADE_EGARCH-t
```
Saída:
```text
Volatilidades_EGARCH_t_1W1M1Y.xlsx
```
---
5.3 GJR-GARCH
Notebook:
```text
CÁLCULO_VOLATILIDADE_GJR.ipynb
```
Saída:
```text
PLD_volatilidades_GJR.xlsx
```
---
5.4 GJR-GARCH-t
Notebook:
```text
CÁLCULO_VOLATILIDADE_GJR_t.ipynb
```
Saída:
```text
PLD_volatilidades_GJR-t.xlsx
```
---
5.5 HAR-RV
Notebook:
```text
CÁLCULO_VOLATILIDADE_HAR_RV.ipynb
```
Saída:
```text
PLD_volatilidades_HAR-RV.xlsx
```
---
6. Observações Importantes — Parte 1
As pastas dos cinco modelos são independentes.
Cada pasta contém os respectivos dados de entrada necessários para a estimação do modelo.
Os arquivos de preços do PLD utilizados como entrada devem permanecer na pasta correspondente ao modelo.
Recomenda-se não alterar os nomes das colunas das planilhas de entrada sem realizar a correspondente atualização no código Python.
As unidades das volatilidades devem ser verificadas antes da utilização na Parte 2, principalmente quanto à distinção entre decimal e percentual.
Deve-se verificar também se a volatilidade utilizada está em escala diária, de horizonte ou anualizada, evitando incompatibilidade de escala na precificação.
---
PARTE 2 — Precificação de Opções de Energia sobre o PLD via Monte Carlo e Modelos Avançados de Volatilidade
7. Descrição Geral
A Parte 2 implementa um pipeline completo para a precificação de opções CALL e PUT sobre o PLD utilizando o Método de Monte Carlo.
São consideradas duas abordagens:
Opção A — Monte Carlo com Volatilidade Constante
Utiliza uma volatilidade anualizada constante correspondente ao horizonte da opção.
Opção B — Monte Carlo com Volatilidade Dinâmica
Utiliza uma trajetória de volatilidade diária dinâmica:
[
\sigma = \sigma(t)
]
A finalidade é avaliar se a utilização da dinâmica temporal da volatilidade melhora a precificação das opções em relação à abordagem de volatilidade constante.
---
8. Modelos de Volatilidade Utilizados
A precificação utiliza os resultados provenientes dos cinco modelos estimados na Parte 1:
HAR-RV
EGARCH
GJR-GARCH
EGARCH-t
GJR-GARCH-t
As séries produzidas pelos modelos podem incluir:
volatilidade diária;
volatilidade semanal;
volatilidade mensal;
volatilidade anual;
volatilidade anualizada por horizonte.
---
9. Horizontes das Opções
Os horizontes considerados na precificação são:
Horizonte	Dias úteis	Tempo em anos
1W	5	5/252
1M	21	21/252
1Y	252	252/252
---
10. Resultados Calculados pelo Pipeline
O pipeline da Parte 2 calcula e consolida:
preços das opções CALL via Monte Carlo;
preços das opções PUT via Monte Carlo;
payoff realizado das opções;
erros de precificação de CALL;
erros de precificação de PUT;
RMSE;
MAE;
MAPE;
SMAPE;
rankings por ano;
rankings por horizonte;
rankings por modelo de volatilidade;
comparação entre as Opções A e B;
heatmaps;
análise da relação entre volatilidade e erros de precificação;
dashboard Excel;
dashboard interativo Plotly em HTML;
relatório técnico final em Word;
relatório técnico final em PDF, quando disponível.
---
11. Requisitos de Pacotes Python
Instale as dependências com:
```bash
pip install pandas numpy matplotlib seaborn plotly xlsxwriter openpyxl python-docx docx2pdf pyarrow
```
> **Importante:** `pyarrow` é necessário para leitura e gravação eficiente do arquivo intermediário no formato `.parquet`.
Para conversão automática do relatório DOCX para PDF:
```bash
pip install docx2pdf
```
---
12. Estrutura de Pastas
```text
Projeto_MC_VOL/
│
├── 01_importacao_merge.py
├── 02_MC_A_sigma_constante.py
├── 03_MC_B_sigma_dinamica.py
├── 04_metricas.py
├── 05_dashboards_excel.py
├── 06_heatmaps.py
├── 07_correlacao_sigma_erros.py
├── 08_dashboard_plotly.py
├── 09_relatorio_final_tese.py
│
├── dados/
│   ├── Volatilidades_HAR_RV_1W1M1Y.xlsx
│   ├── Volatilidades_EGARCH_1W1M1Y.xlsx
│   ├── Volatilidades_GJR_1W1M1Y.xlsx
│   ├── Volatilidades_EGARCH_t_1W1M1Y.xlsx
│   └── Volatilidades_GJR_t_1W1M1Y.xlsx
│
├── RESULTADOS_MC_OPCAO_A/
├── RESULTADOS_MC_OPCAO_B/
├── METRICAS_MC/
├── HEATMAPS_MC/
├── CORRELACAO_SIGMA/
├── DASHBOARDS/
└── RELATORIOS/
```
---
13. Ordem de Execução dos Módulos
> **IMPORTANTE:** a ordem de execução deve ser respeitada para garantir a consistência dos dados e a reprodutibilidade dos resultados.
---
13.1 Módulo 01 — Importação e Merge das Séries de Volatilidade
Execute:
```bash
python 01_importacao_merge.py
```
Saída principal:
```text
df_vols_merged.parquet
```
Função
Este módulo realiza:
leitura das cinco bases de volatilidade;
padronização das datas;
padronização das colunas;
verificação das séries;
merge das volatilidades;
geração da base consolidada utilizada pelos módulos posteriores.
---
13.2 Módulo 02 — Monte Carlo com σ Constante — Opção A
Execute:
```bash
python 02_MC_A_sigma_constante.py
```
Saídas:
```text
RESULTADOS_MC_OPCAO_A/
├── Opcoes_MC_Constante_2019.xlsx
├── Opcoes_MC_Constante_2020.xlsx
├── Opcoes_MC_Constante_2021.xlsx
├── Opcoes_MC_Constante_2022.xlsx
├── Opcoes_MC_Constante_2023.xlsx
├── Opcoes_MC_Constante_2024.xlsx
└── Opcoes_MC_Constante_2019_2024_CONSOLIDADO.xlsx
```
Função
Realiza a precificação das opções utilizando uma volatilidade anualizada constante para cada horizonte.
---
13.3 Módulo 03 — Monte Carlo com σ Dinâmica — Opção B
Execute:
```bash
python 03_MC_B_sigma_dinamica.py
```
Saídas:
```text
RESULTADOS_MC_OPCAO_B/
├── Opcoes_MC_Dinamica_2019.xlsx
├── Opcoes_MC_Dinamica_2020.xlsx
├── Opcoes_MC_Dinamica_2021.xlsx
├── Opcoes_MC_Dinamica_2022.xlsx
├── Opcoes_MC_Dinamica_2023.xlsx
├── Opcoes_MC_Dinamica_2024.xlsx
└── Opcoes_MC_Dinamica_2019_2024_CONSOLIDADO.xlsx
```
Função
Realiza a precificação utilizando uma trajetória de volatilidade diária dinâmica, representada por:
[
\sigma(t)
]
para cada período de vida da opção.
---
13.4 Módulo 04 — Cálculo das Métricas
Execute:
```bash
python 04_metricas.py
```
São calculadas as principais métricas de erro:
[
RMSE =
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
(\hat{y}_i-y_i)^2
}
]
[
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
|\hat{y}_i-y_i|
]
Além de:
MAPE;
SMAPE.
Saídas:
```text
METRICAS_MC/
├── Metricas_MC.xlsx
└── Rankings_MC.xlsx
```
---
13.5 Módulo 05 — Dashboard Excel
Execute:
```bash
python 05_dashboards_excel.py
```
Saída:
```text
DASHBOARDS/
└── Dashboard_Opcoes_MC.xlsx
```
O dashboard consolida os principais resultados da precificação e das métricas de desempenho.
---
13.6 Módulo 06 — Heatmaps Avançados
Execute:
```bash
python 06_heatmaps.py
```
Saídas:
```text
HEATMAPS_MC/
├── RMSE/
│   └── *.png
├── MAE/
│   └── *.png
├── MAPE/
│   └── *.png
├── SMAPE/
│   └── *.png
└── COMPARATIVO_A_B/
    └── *.png
```
Os heatmaps permitem identificar visualmente:
melhores modelos;
piores modelos;
diferenças entre anos;
diferenças entre horizontes;
diferenças entre CALL e PUT;
diferenças entre Monte Carlo A e Monte Carlo B.
---
13.7 Módulo 07 — Correlação entre Erro de Volatilidade e Erro das Opções
Execute:
```bash
python 07_correlacao_sigma_erros.py
```
Saídas:
```text
CORRELACAO_SIGMA/
├── Correlacoes_sigma_erros.csv
└── SCATTERS/
    └── *.png
```
Objetivo
Investigar se os erros associados às estimativas de volatilidade apresentam relação estatística com os erros observados na precificação das opções.
---
13.8 Módulo 08 — Dashboard Interativo Plotly
Execute:
```bash
python 08_dashboard_plotly.py
```
Saída:
```text
DASHBOARDS/
└── dashboard_plotly_opcoes_mc.html
```
O arquivo HTML pode ser aberto diretamente em um navegador compatível.
---
13.9 Módulo 09 — Relatório Final Unificado
Execute:
```bash
python 09_relatorio_final_tese.py
```
Saídas:
```text
RELATORIOS/
├── Relatorio_Final_Opcoes_MC.docx
└── Relatorio_Final_Opcoes_MC.pdf
```
O arquivo PDF será produzido automaticamente apenas quando o ambiente possuir suporte adequado à conversão.
---
14. Fluxo Geral do Projeto
O fluxo completo pode ser representado da seguinte forma:
```text
PREÇOS DIÁRIOS DO PLD
        │
        ▼
VOLATILIDADE REALIZADA
        │
        ├───────────────┬───────────────┬───────────────┬───────────────┐
        ▼               ▼               ▼               ▼               ▼
     HAR-RV          EGARCH         GJR-GARCH        EGARCH-t      GJR-GARCH-t
        │               │               │               │               │
        └───────────────┴───────────────┴───────────────┴───────────────┘
                                │
                                ▼
                    BASE DE VOLATILIDADES
                                │
                                ▼
                    01_importacao_merge.py
                                │
                                ▼
                   df_vols_merged.parquet
                                │
                  ┌─────────────┴─────────────┐
                  ▼                           ▼
             OPÇÃO A                      OPÇÃO B
          σ CONSTANTE                  σ(t) DINÂMICA
                  │                           │
                  ▼                           ▼
             MONTE CARLO                  MONTE CARLO
                  │                           │
                  └─────────────┬─────────────┘
                                ▼
                         CALL / PUT
                                │
                                ▼
                       PAYOFF REALIZADO
                                │
                                ▼
                          ERROS A / B
                                │
                                ▼
                  RMSE / MAE / MAPE / SMAPE
                                │
               ┌────────────────┼─────────────────┐
               ▼                ▼                 ▼
            RANKINGS         HEATMAPS        CORRELAÇÕES
               │                │                 │
               └────────────────┼─────────────────┘
                                ▼
                         DASHBOARDS
                                │
                                ▼
                      RELATÓRIO FINAL
```
---
15. Reprodutibilidade
Para garantir a reprodutibilidade dos experimentos, recomenda-se:
utilizar sempre a mesma base de preços do PLD;
preservar os nomes e formatos das colunas;
manter os parâmetros dos modelos documentados;
registrar a versão dos pacotes Python utilizados;
utilizar uma semente aleatória fixa nas simulações de Monte Carlo;
manter constante o número de simulações quando forem realizadas comparações entre modelos;
verificar as unidades das volatilidades antes da precificação;
manter os mesmos períodos de início e vencimento para comparações entre modelos;
não alterar os arquivos intermediários manualmente;
executar os módulos da Parte 2 na ordem estabelecida.
Uma forma recomendada de registrar as dependências é:
```bash
pip freeze > requirements.txt
```
Posteriormente, o ambiente pode ser reconstruído utilizando:
```bash
pip install -r requirements.txt
```
---
16. Observações Importantes — Parte 2
Os módulos possuem funções específicas, mas fazem parte de um pipeline sequencial.
A pasta `dados/` deve conter as cinco planilhas de volatilidade geradas ou padronizadas a partir da Parte 1.
Os nomes das colunas de volatilidade devem ser compatíveis com aqueles esperados pelos módulos Python.
Todos os caminhos utilizados pelos códigos devem ser preferencialmente relativos à pasta raiz do projeto.
Caso a estrutura de diretórios seja alterada, os caminhos definidos nos scripts também deverão ser atualizados.
A conversão automática de DOCX para PDF depende do ambiente operacional e dos softwares instalados.
Em ambientes nos quais `docx2pdf` não esteja disponível, o relatório DOCX poderá ser convertido posteriormente para PDF.
As comparações entre as Opções A e B devem utilizar exatamente os mesmos contratos, datas, parâmetros financeiros e configurações de simulação.
Recomenda-se fixar a semente pseudoaleatória do Monte Carlo para tornar as comparações reproduzíveis.
---
17. Resumo da Arquitetura
```text
PARTE 1
│
├── HAR-RV
├── EGARCH
├── GJR-GARCH
├── EGARCH-t
└── GJR-GARCH-t
        │
        ▼
PLANILHAS DE VOLATILIDADE
        │
        ▼
PARTE 2
│
├── 01 - Importação e Merge
├── 02 - Monte Carlo A: σ Constante
├── 03 - Monte Carlo B: σ(t) Dinâmica
├── 04 - Métricas
├── 05 - Dashboard Excel
├── 06 - Heatmaps
├── 07 - Correlação σ × Erros
├── 08 - Dashboard Plotly
└── 09 - Relatório Final
        │
        ▼
RESULTADOS CONSOLIDADOS
```
---
18. Estrutura Metodológica Resumida
A metodologia geral do projeto pode ser sintetizada por:
[
PLD_t
\rightarrow
RV_t
\rightarrow
\sigma_t
\rightarrow
MC
\rightarrow
(CALL,PUT)
\rightarrow
Payoff_{realizado}
\rightarrow
Erro
\rightarrow
Métricas
\rightarrow
Ranking
]
onde:
(PLD_t) = preço diário do PLD;
(RV_t) = volatilidade realizada;
(\sigma_t) = volatilidade condicional estimada;
(MC) = simulação de Monte Carlo;
(CALL) = prêmio estimado da opção de compra;
(PUT) = prêmio estimado da opção de venda;
(Payoff_{realizado}) = payoff calculado a partir do preço observado no vencimento;
(Erro) = diferença entre a estimativa do modelo e a referência empírica adotada;
(Métricas) = RMSE, MAE, MAPE e SMAPE;
(Ranking) = classificação dos modelos segundo seu desempenho.
---
19. Arquitetura Completa
```text
┌─────────────────────────────────────────────┐
│              BASE DIÁRIA DO PLD             │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│          VOLATILIDADE REALIZADA DO PLD      │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│          MODELOS DE VOLATILIDADE            │
│                                             │
│ HAR-RV | EGARCH | GJR | EGARCH-t | GJR-t   │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│        VOLATILIDADES 1W / 1M / 1Y           │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│           PRECIFICAÇÃO MONTE CARLO          │
│                                             │
│       OPÇÃO A            OPÇÃO B            │
│      σ constante         σ(t) dinâmica      │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│               CALL / PUT                    │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│             PAYOFF REALIZADO                │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│           ERROS DE PRECIFICAÇÃO             │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│       RMSE | MAE | MAPE | SMAPE             │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│ RANKINGS | HEATMAPS | CORRELAÇÕES | PAINÉIS│
└─────────────────────┬───────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────┐
│            RELATÓRIO FINAL                  │
└─────────────────────────────────────────────┘
```
---
20. Considerações Finais
O projeto estabelece uma arquitetura integrada para estudar a influência da modelagem da volatilidade na precificação estocástica de opções sobre o PLD.
A Parte 1 é responsável pela estimação e organização das volatilidades condicionais provenientes dos modelos HAR-RV, EGARCH, GJR-GARCH, EGARCH-t e GJR-GARCH-t.
A Parte 2 utiliza essas volatilidades como entradas para duas estratégias de precificação via Monte Carlo:
Opção A: volatilidade anualizada constante;
Opção B: volatilidade diária dinâmica (\sigma(t)).
Os resultados são posteriormente avaliados por meio de métricas de erro, rankings, heatmaps, análises de correlação e dashboards, permitindo comparar sistematicamente os modelos de volatilidade e as duas abordagens de Monte Carlo.
---
Fim do README
Projeto: Precificação Estocástica de Opções sobre o PLD com Volatilidades HAR-RV, EGARCH, GJR-GARCH, EGARCH-t e GJR-GARCH-t  
Autor: Prof. Paulo Cavalcante  
Versão: 2026
