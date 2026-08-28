=============================================================
PROJETO PARTE 1: Cálculo de Volatilidades Condicional
Estocásticas com Base na Volatilidade Diária do PLD
=============================================================

Autor: Prof. Paulo Cavalcante
Versão: 2026
Arquitetura: 5 Códigos Python independentes, 1 para cada modelo

-------------------------------------------------------------
DESCRIÇÃO GERAL DO PROJETO
-------------------------------------------------------------
O programa tem como objetivo central estimar a volatilidade condicional do Preço de Liquidação das Diferenças (PLD) para o Submercado Sudeste do Sistema Interligado Nacional (SIN), utilizando os 5 modelos de volatilidade condicional estocástica (HAR-RV, EGARCH, GJR, EGARCH-t e GJR-t), a partir das volatilidades diárias realizadas do PLD:

Cada modelo produz:
	- volatilidades realizada PLD
	- volatilidade diárias de cada modelo
	- volatilidade mensal de cada modelo
	- volatilidade anual de cada modelo
	- volatilidade anualizada de cada modelo

-------------------------------------------------------------
REQUISITOS DE PACOTES PYTHON
-------------------------------------------------------------

pip install pandas numpy math scipy arch openpyxl os matplotlib seaborn plotly xlsxwriter docx docx2pdf warnings datetime

Se quiser converter automaticamente para PDF:
pip install docx2pdf
(Windows recomendado)

-------------------------------------------------------------
ESTRUTURA DE PASTAS
-------------------------------------------------------------

/1-CALCULO_VOLATILIDADES/
	/EGARCH/
		CÁLCULO_VOLATILIDADE_EGARCH.ipynb
		PLD_volatilidades_EGARCH
		PREÇO MED DIARIO PLD  VERTICAL PERIODO 17-04-18 A 03-06-25
	/EGARCH-t/
		CÁLCULO VOLATILIDADE_EGARCH-t
		Volatilidades_EGARCH_t_1W1M1Y
		PREÇO MED DIARIO PLD  VERTICAL PERIODO 17-04-18 A 03-06-25
	/GJR/
		CÁLCULO_VOLATILIDADE_GJR.ipynb
		PLD_volatilidades_GJR
		PREÇO MED DIARIO PLD  VERTICAL PERIODO 17-04-18 A 03-06-25
	/GJR-t/
		CÁLCULO_VOLATILIDADE_GJR_t.ipynb
		PLD_volatilidades_GJR-t
		PREÇO MED DIARIO PLD  VERTICAL PERIODO 17-04-18 A 03-06-25
	/HAR-RV/
		CÁLCULO_VOLATILIDADE_HAR_RV.ipynb
		PLD_volatilidades_HAR-RV
		PREÇO MED DIARIO PLD  VERTICAL PERIODO 17-04-18 A 03-06-25

-------------------------------------------------------------
EXECUÇÃO DOS CÓDIGOS
-------------------------------------------------------------

=============================================================
1) EGARCH
=============================================================
notebook CÁLCULO_VOLATILIDADE_EGARCH.ipynb

Saída:
    PLD_volatilidades_EGARCHC.xlsx
=============================================================
1) EGARCH-t
=============================================================
notebook CÁLCULO VOLATILIDADE_EGARCH-t

Saída:
    Volatilidades_EGARCH_t_1W1M1Y.xlsx
=============================================================
1) GJR
=============================================================
notebook CÁLCULO_VOLATILIDADE_GJR.ipynb

Saída:
    PLD_volatilidades_GJR.xlsx
=============================================================
1) GJR-t
=============================================================
notebook CÁLCULO_VOLATILIDADE_GJR_t.ipynb

Saída:
    PLD_volatilidades_GJR-t.xlsx
=============================================================
1) HAR-RV
=============================================================
notebook CÁLCULO_VOLATILIDADE_HAR_RV.ipynb

Saída:
    PLD_volatilidades_HAR-RV.xlsx

OBSERVAÇÕES IMPORTANTES
-------------------------------------------------------------

• Os pastas são independentes

• Os dados de entrada encontram-se nas pastas de cada volatilidade.

=============================================================
PROJETO PARTE 2: Precificação de Opções de Energia (PLD)
         via Monte Carlo + Modelos Avançados de Volatilidade
=============================================================

Autor: Prof. Paulo Cavalcante
Versão: 2026
Arquitetura Modular (9 Módulos Python)

-------------------------------------------------------------
DESCRIÇÃO GERAL DO PROJETO
-------------------------------------------------------------
Este projeto implementa um pipeline completo para precificação
de opções CALL e PUT sobre o PLD (Preço de Liquidação das Diferenças)
utilizando o Método de Monte Carlo, com duas abordagens:

  - OPÇÃO A → Monte Carlo com volatilidade anualizada constante
  - OPÇÃO B → Monte Carlo com volatilidade diária dinâmica (σ(t))

Cinco modelos de volatilidade são considerados:
    1. HAR-RV
    2. EGARCH
    3. GJR
    4. EGARCH-t
    5. GJR-t

Cada modelo produz:
    - volatilidade diária
    - volatilidade semanal, mensal, anual
    - volatilidade anualizada por janela

O pipeline calcula:
    - Preços CALL / PUT (MC)
    - Payoff realizado
    - Erros (CALL/PUT)
    - Métricas (RMSE, MAE, MAPE, SMAPE)
    - Rankings por ano/horizonte/modelo
    - Heatmaps
    - Dashboard Excel
    - Dashboard Plotly (HTML)
    - Relatório técnico completo (Word/PDF)

-------------------------------------------------------------
REQUISITOS DE PACOTES PYTHON
-------------------------------------------------------------

pip install pandas numpy matplotlib seaborn plotly xlsxwriter docx docx2pdf

Se quiser converter automaticamente para PDF:
pip install docx2pdf
(Windows recomendado)

-------------------------------------------------------------
ESTRUTURA DE PASTAS
-------------------------------------------------------------

/Projeto_MC_VOL/
    01_importacao_merge.py
    02_MC_A_sigma_constante.py
    03_MC_B_sigma_dinamica.py
    04_metricas.py
    05_dashboards_excel.py
    06_heatmaps.py
    07_correlacao_sigma_erros.py
    08_dashboard_plotly.py
    09_relatorio_final_tese.py

    /dados/
        Volatilidades_HAR_RV_1W1M1Y.xlsx
        Volatilidades_EGARCH_1W1M1Y.xlsx
        Volatilidades_GJR_1W1M1Y.xlsx
        Volatilidades_EGARCH_t_1W1M1Y.xlsx
        Volatilidades_GJR_t_1W1M1Y.xlsx

    /RESULTADOS_MC_OPCAO_A/
    /RESULTADOS_MC_OPCAO_B/
    /METRICAS_MC/
    /HEATMAPS_MC/
    /CORRELACAO_SIGMA/
    /DASHBOARDS/
    /RELATORIOS/

-------------------------------------------------------------
ORDEM DE EXECUÇÃO DOS MÓDULOS
-------------------------------------------------------------

A ORDEM É OBRIGATÓRIA PARA GARANTIR REPRODUTIBILIDADE:

=============================================================
1) Importação e merge das séries de volatilidade
=============================================================
python 01_importacao_merge.py

Saída gerada:
    - df_vols_merged.parquet

=============================================================
2) Monte Carlo com σ CONSTANTE (OPÇÃO A)
=============================================================
python 02_MC_A_sigma_constante.py

Saídas:
    /RESULTADOS_MC_OPCAO_A/
         Opcoes_MC_Constante_2019.xlsx
         ...
         Opcoes_MC_Constante_2024.xlsx
         Opcoes_MC_Constante_2019_2024_CONSOLIDADO.xlsx

=============================================================
3) Monte Carlo com σ DINÂMICA (OPÇÃO B)
=============================================================
python 03_MC_B_sigma_dinamica.py

Saídas:
    /RESULTADOS_MC_OPCAO_B/
         Opcoes_MC_Dinamica_2019.xlsx
         ...
         Opcoes_MC_Dinamica_2024.xlsx
         Opcoes_MC_Dinamica_2019_2024_CONSOLIDADO.xlsx

=============================================================
4) Cálculo de métricas (RMSE, MAE, MAPE, SMAPE)
=============================================================
python 04_metricas.py

Saídas:
    /METRICAS_MC/Metricas_MC.xlsx
    /METRICAS_MC/Rankings_MC.xlsx

=============================================================
5) Dashboard Excel com slicers
=============================================================
python 05_dashboards_excel.py

Saída:
    /DASHBOARDS/Dashboard_Opcoes_MC.xlsx

=============================================================
6) Heatmaps avançados (Métricas + A vs B)
=============================================================
python 06_heatmaps.py

Saídas:
    /HEATMAPS_MC/RMSE/*.png
    /HEATMAPS_MC/MAE/*.png
    /HEATMAPS_MC/MAPE/*.png
    /HEATMAPS_MC/SMAPE/*.png
    /HEATMAPS_MC/COMPARATIVO_A_B/*.png

=============================================================
7) Correlação entre erro de sigma e erro de opções
=============================================================
python 07_correlacao_sigma_erros.py

Saídas:
    /CORRELACAO_SIGMA/Correlacoes_sigma_erros.csv
    /CORRELACAO_SIGMA/SCATTERS/*.png

=============================================================
8) Dashboard interativo Plotly (HTML)
=============================================================
python 08_dashboard_plotly.py

Saída:
    /DASHBOARDS/dashboard_plotly_opcoes_mc.html

=============================================================
9) Relatório final unificado (Word/PDF)
=============================================================
python 09_relatorio_final_tese.py

Saídas:
    /RELATORIOS/Relatorio_Final_Opcoes_MC.docx
    /RELATORIOS/Relatorio_Final_Opcoes_MC.pdf (se docx2pdf disponível)


-------------------------------------------------------------
OBSERVAÇÕES IMPORTANTES
-------------------------------------------------------------

• Os módulos são independentes, mas devem ser executados
  *na ordem definida*.

• A pasta /dados/ deve conter as 5 planilhas originais
  com as volatilidades (HAR, EGARCH, etc).

• A conversão automática para PDF depende do Windows.
  Em Linux/Mac, abra o DOCX e exporte manualmente.

• Todos os caminhos são relativos à pasta raiz
  do projeto. Altere se necessário.

=============================================================
FIM DO README
=============================================================
