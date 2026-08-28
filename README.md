Projeto de Volatilidade e Precificação de Opções de Energia (PLD)
Autor: Prof. Paulo Cavalcante
Versão: 2026

Este repositório está dividido em duas partes principais:

Parte 1: Cálculo de volatilidades condicionais estocásticas com base na volatilidade diária realizada do PLD.
Parte 2: Precificação de opções de energia sobre o PLD via Monte Carlo, utilizando os modelos de volatilidade calculados na Parte 1.
PARTE 1 — Cálculo de Volatilidades Condicionais Estocásticas
1. Descrição Geral
O objetivo da Parte 1 é estimar a volatilidade condicional do Preço de Liquidação das Diferenças (PLD) para o Submercado Sudeste do Sistema Interligado Nacional (SIN).

São utilizados cinco modelos de volatilidade:

HAR-RV
EGARCH
GJR
EGARCH-t
GJR-t
Os modelos utilizam como base as séries de volatilidade diária realizada do PLD.

Cada modelo produz:

volatilidade realizada do PLD;
volatilidade diária estimada pelo modelo;
volatilidade semanal;
volatilidade mensal;
volatilidade anual;
volatilidade anualizada por janela.
A arquitetura da Parte 1 é composta por 5 códigos independentes, sendo um para cada modelo.

2. Requisitos de Pacotes Python
Instale os principais pacotes utilizados no projeto:

pip install pandas numpy scipy arch openpyxl matplotlib seaborn plotly xlsxwriter python-docx docx2pdf

Observação: math, os, warnings e datetime são módulos da biblioteca padrão do Python e não precisam ser instalados via pip.

Conversão automática para PDF
Para gerar automaticamente o relatório em PDF a partir do DOCX:

pip install docx2pdf

Windows: recomendado para a conversão automática utilizando o docx2pdf.

3. Estrutura de Pastas
/1-CALCULO_VOLATILIDADES/
│
├── EGARCH/
│   ├── CALCULO_VOLATILIDADE_EGARCH.ipynb
│   ├── PLD_volatilidades_EGARCH.xlsx
│   └── PRECO_MED_DIARIO_PLD_VERTICAL_PERIODO_17-04-18_A_03-06-25.xlsx
│
├── EGARCH-t/
│   ├── CALCULO_VOLATILIDADE_EGARCH-t.ipynb
│   ├── Volatilidades_EGARCH_t_1W1M1Y.xlsx
│   └── PRECO_MED_DIARIO_PLD_VERTICAL_PERIODO_17-04-18_A_03-06-25.xlsx
│
├── GJR/
│   ├── CALCULO_VOLATILIDADE_GJR.ipynb
│   ├── PLD_volatilidades_GJR.xlsx
│   └── PRECO_MED_DIARIO_PLD_VERTICAL_PERIODO_17-04-18_A_03-06-25.xlsx
│
├── GJR-t/
│   ├── CALCULO_VOLATILIDADE_GJR_t.ipynb
│   ├── PLD_volatilidades_GJR-t.xlsx
│   └── PRECO_MED_DIARIO_PLD_VERTICAL_PERIODO_17-04-18_A_03-06-25.xlsx
│
└── HAR-RV/
    ├── CALCULO_VOLATILIDADE_HAR_RV.ipynb
    ├── PLD_volatilidades_HAR-RV.xlsx
    └── PRECO_MED_DIARIO_PLD_VERTICAL_PERIODO_17-04-18_A_03-06-25.xlsx

Os nomes acima foram padronizados para facilitar a leitura. Caso os arquivos reais tenham nomes diferentes, mantenha no README os nomes exatamente iguais aos existentes no repositório.

4. Execução dos Modelos
Cada modelo da Parte 1 pode ser executado de forma independente.

4.1 EGARCH
Notebook:

CALCULO_VOLATILIDADE_EGARCH.ipynb

Saída principal:

PLD_volatilidades_EGARCH.xlsx

4.2 EGARCH-t
Notebook:

CALCULO_VOLATILIDADE_EGARCH-t.ipynb

Saída principal:

Volatilidades_EGARCH_t_1W1M1Y.xlsx

4.3 GJR
Notebook:

CALCULO_VOLATILIDADE_GJR.ipynb

Saída principal:

PLD_volatilidades_GJR.xlsx

4.4 GJR-t
Notebook:

CALCULO_VOLATILIDADE_GJR_t.ipynb

Saída principal:

PLD_volatilidades_GJR-t.xlsx

4.5 HAR-RV
Notebook:

CALCULO_VOLATILIDADE_HAR_RV.ipynb

Saída principal:

PLD_volatilidades_HAR-RV.xlsx

5. Observações Importantes — Parte 1
As pastas dos modelos são independentes.
Cada modelo possui seu próprio código/notebook.
Os dados de entrada encontram-se nas respectivas pastas dos modelos.
As planilhas geradas na Parte 1 são utilizadas como entrada para a Parte 2.
Recomenda-se manter os arquivos de entrada e saída organizados dentro das respectivas pastas.
PARTE 2 — Precificação de Opções de Energia sobre o PLD
6. Descrição Geral
A Parte 2 implementa um pipeline completo para precificação de opções CALL e PUT sobre o PLD, utilizando o Método de Monte Carlo e os modelos de volatilidade estimados na Parte 1.

São consideradas duas abordagens principais:

Opção A — Volatilidade Anualizada Constante
O processo de Monte Carlo utiliza uma volatilidade anualizada constante:

σ(t) = σ_anualizado

Opção B — Volatilidade Diária Dinâmica
O processo de Monte Carlo utiliza uma volatilidade que varia ao longo do tempo:

σ(t) = volatilidade diária dinâmica

7. Modelos de Volatilidade
A Parte 2 utiliza os cinco modelos calculados na Parte 1:

HAR-RV
EGARCH
GJR
EGARCH-t
GJR-t
Cada modelo fornece informações de volatilidade em diferentes horizontes:

diária;
semanal;
mensal;
anual;
anualizada por janela.
8. Resultados Gerados
O pipeline da Parte 2 calcula e/ou gera:

preços de opções CALL;
preços de opções PUT;
payoff realizado;
erros de precificação de CALL;
erros de precificação de PUT;
RMSE;
MAE;
MAPE;
SMAPE;
rankings por ano;
rankings por horizonte;
rankings por modelo;
heatmaps de desempenho;
comparação entre as abordagens A e B;
análise de correlação entre erro de volatilidade e erro de precificação;
dashboard Excel;
dashboard interativo em Plotly/HTML;
relatório técnico completo em Word/PDF.
9. Requisitos de Pacotes Python
Instale os pacotes necessários:

pip install pandas numpy matplotlib seaborn plotly xlsxwriter python-docx docx2pdf

Para conversão automática do relatório para PDF:

pip install docx2pdf

Observação: a conversão automática via docx2pdf é recomendada em ambiente Windows.

10. Estrutura de Pastas da Parte 2
/Projeto_MC_VOL/
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
│
├── RESULTADOS_MC_OPCAO_B/
│
├── METRICAS_MC/
│
├── HEATMAPS_MC/
│
├── CORRELACAO_SIGMA/
│
├── DASHBOARDS/
│
└── RELATORIOS/

11. Ordem de Execução dos Módulos
IMPORTANTE: a ordem de execução é obrigatória para garantir a correta geração dos arquivos intermediários e a reprodutibilidade dos resultados.

11.1 Importação e Merge das Séries de Volatilidade
Script:

python 01_importacao_merge.py

Função:

Importa as séries de volatilidade dos cinco modelos e realiza a consolidação das informações em uma única base.

Saída:

df_vols_merged.parquet

11.2 Monte Carlo com Volatilidade Constante — Opção A
Script:

python 02_MC_A_sigma_constante.py

Função:

Realiza a precificação das opções utilizando volatilidade anualizada constante.

Saídas:

RESULTADOS_MC_OPCAO_A/
├── Opcoes_MC_Constante_2019.xlsx
├── ...
├── Opcoes_MC_Constante_2024.xlsx
└── Opcoes_MC_Constante_2019_2024_CONSOLIDADO.xlsx

11.3 Monte Carlo com Volatilidade Dinâmica — Opção B
Script:

python 03_MC_B_sigma_dinamica.py

Função:

Realiza a precificação das opções utilizando volatilidade diária dinâmica.

Saídas:

RESULTADOS_MC_OPCAO_B/
├── Opcoes_MC_Dinamica_2019.xlsx
├── ...
├── Opcoes_MC_Dinamica_2024.xlsx
└── Opcoes_MC_Dinamica_2019_2024_CONSOLIDADO.xlsx

11.4 Cálculo das Métricas
Script:

python 04_metricas.py

Função:

Calcula as métricas de erro utilizadas para avaliar o desempenho dos modelos.

Métricas:

RMSE — Root Mean Squared Error;
MAE — Mean Absolute Error;
MAPE — Mean Absolute Percentage Error;
SMAPE — Symmetric Mean Absolute Percentage Error.
Saídas:

METRICAS_MC/
├── Metricas_MC.xlsx
└── Rankings_MC.xlsx

11.5 Dashboard Excel
Script:

python 05_dashboards_excel.py

Função:

Gera o dashboard consolidado em Excel, incluindo os recursos de análise e filtros disponíveis no arquivo.

Saída:

DASHBOARDS/
└── Dashboard_Opcoes_MC.xlsx

11.6 Heatmaps Avançados
Script:

python 06_heatmaps.py

Função:

Gera heatmaps para análise das métricas de desempenho e comparação entre as abordagens de Monte Carlo.

Saídas:

HEATMAPS_MC/
├── RMSE/
│   └── *.png
│
├── MAE/
│   └── *.png
│
├── MAPE/
│   └── *.png
│
├── SMAPE/
│   └── *.png
│
└── COMPARATIVO_A_B/
    └── *.png

11.7 Correlação entre Erro de Volatilidade e Erro de Opções
Script:

python 07_correlacao_sigma_erros.py

Função:

Analisa a relação entre os erros associados às estimativas de volatilidade e os erros de precificação das opções.

Saídas:

CORRELACAO_SIGMA/
├── Correlacoes_sigma_erros.csv
└── SCATTERS/
    └── *.png

11.8 Dashboard Interativo em Plotly
Script:

python 08_dashboard_plotly.py

Função:

Gera um dashboard interativo para exploração dos resultados de precificação e desempenho dos modelos.

Saída:

DASHBOARDS/
└── dashboard_plotly_opcoes_mc.html

O arquivo HTML pode ser aberto diretamente em um navegador.

11.9 Relatório Final Unificado
Script:

python 09_relatorio_final_tese.py

Função:

Consolida os principais resultados do projeto em um relatório técnico destinado à documentação e análise dos resultados.

Saídas:

RELATORIOS/
├── Relatorio_Final_Opcoes_MC.docx
└── Relatorio_Final_Opcoes_MC.pdf

O arquivo PDF será gerado automaticamente caso o docx2pdf esteja instalado e o ambiente seja compatível.

12. Fluxo Geral do Projeto
O fluxo completo pode ser resumido da seguinte forma:

                    PARTE 1
                       │
                       ▼
          ┌─────────────────────────┐
          │ Modelos de Volatilidade │
          └─────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
     HAR-RV         EGARCH           GJR
        │              │              │
        └──────────────┼──────────────┘
                       │
                EGARCH-t / GJR-t
                       │
                       ▼
             Séries de Volatilidade
                       │
                       ▼
                    PARTE 2
                       │
                       ▼
              01_importacao_merge
                       │
                       ▼
             ┌─────────┴─────────┐
             │                   │
             ▼                   ▼
       OPÇÃO A               OPÇÃO B
   σ anualizada            σ dinâmica
     constante               diária
             │                   │
             └─────────┬─────────┘
                       ▼
                04_metricas
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
          Rankings  Heatmaps  Correlações
             │         │         │
             └─────────┼─────────┘
                       ▼
              Dashboards / Plotly
                       │
                       ▼
                Relatório Final

13. Observações Importantes
Os cinco modelos da Parte 1 são independentes entre si.
Os resultados da Parte 1 constituem os principais dados de entrada da Parte 2.
A pasta dados/ deve conter as cinco planilhas de volatilidade necessárias para a execução da Parte 2.
Os módulos da Parte 2 devem ser executados na ordem definida neste README.
Os caminhos utilizados pelos scripts são relativos à pasta raiz do projeto.
Caso a estrutura de diretórios seja alterada, os caminhos dos scripts deverão ser ajustados.
A geração do relatório em PDF depende da disponibilidade e configuração do docx2pdf.
Em ambientes Linux/macOS, caso a conversão automática não funcione, o arquivo .docx pode ser aberto em um editor compatível e exportado manualmente para PDF.
Recomenda-se manter os arquivos intermediários e resultados em suas respectivas pastas para facilitar a rastreabilidade e a reprodução dos experimentos.
14. Resumo dos Modelos e Métodos
Categoria	Modelos / Métodos
Volatilidade	HAR-RV
Volatilidade	EGARCH
Volatilidade	GJR
Volatilidade	EGARCH-t
Volatilidade	GJR-t
Precificação	Monte Carlo — σ constante
Precificação	Monte Carlo — σ dinâmica
Métricas	RMSE, MAE, MAPE, SMAPE
Visualização	Heatmaps
Dashboard	Excel
Dashboard	Plotly / HTML
Relatório	Word / PDF

15. Resultado Final
Ao final da execução completa do pipeline, o projeto disponibiliza:

Séries de volatilidade estimadas pelos cinco modelos;
Preços de opções CALL e PUT via Monte Carlo;
Resultados para volatilidade constante e dinâmica;
Métricas de erro de precificação;
Rankings de desempenho;
Heatmaps comparativos;
Análises de correlação;
Dashboard Excel;
Dashboard interativo em Plotly;
Relatório técnico final em Word/PDF.
FIM DO README
