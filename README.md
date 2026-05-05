# 🛑 Fatores de Risco para o Abandono do Tratamento da Tuberculose (SINAN/DataSUS)

Este projeto contém scripts em Python (Jupyter Notebooks) desenvolvidos para automatizar a extração, o processamento e a análise estatística de dados do Sistema de Informação de Agravos de Notificação (SINAN). O objetivo principal é avaliar os determinantes sociodemográficos e clínicos associados ao **abandono do tratamento da Tuberculose** no Brasil.

## 🎯 Objetivo

Facilitar a mineração de dados epidemiológicos públicos e aplicar testes estatísticos para medir a força da associação entre diversas variáveis independentes (ex: uso de drogas, coinfecção por HIV, situação de rua) e o desfecho de abandono do tratamento, gerando planilhas prontas para publicações científicas e relatórios em saúde pública.

## ✨ Funcionalidades

*   **Extração Automatizada:** Download dos arquivos `.dbc` do SINAN via FTP do DATASUS (anos de 2019 a 2022) utilizando a biblioteca `PySUS`.
*   **Limpeza e Estruturação:** Filtragem do desfecho principal na variável `SITUA_ENCE` (comparando "Abandono" vs. "Cura/Óbito"). Exclusão automatizada de registros nulos e ignorados ("Ignorado", "Não se aplica") para evitar viés analítico.
*   **Análise Estatística Avançada:** Cálculo automático de métricas epidemiológicas cruciais para cada variável:
    *   **Frequência Absoluta e Relativa:** Total de casos, total de abandonos e % de abandono.
    *   **Odds Ratio (OR) com IC 95%:** Cálculo da Razão de Chances e seu respectivo Intervalo de Confiança.
    *   **Chi-quadrado ($\chi^2$):** Teste de associação entre as variáveis categóricas.
    *   **Valor-p (*p-value*):** Avaliação da significância estatística das associações.
*   **Exportação em Lote:** Geração individual de planilhas `.xlsx` para cada variável analisada e compactação automática de todos os resultados em um único arquivo `.zip` para download facilitado.

## 📊 Variáveis Analisadas

O script realiza o cruzamento e a análise estatística das seguintes variáveis:
1.  **Sociodemográficas:** Sexo, Faixa Etária, Raça/Cor, Escolaridade.
2.  **Populações Especiais:** População Prisional, População em Situação de Rua, Profissionais de Saúde, Imigrantes.
3.  **Fatores Sociais:** Beneficiários de Programas de Transferência de Renda (Governo).
4.  **Estilo de Vida:** Uso de Drogas Ilícitas, Uso de Álcool, Tabagismo.
5.  **Clínicas e Comorbidades:** Forma da TB (Pulmonar vs. Extrapulmonar), Coinfecção por HIV, Diabetes, Outras Doenças Imunossupressoras.
6.  **Tratamento:** Realização de Tratamento Diretamente Observado (TDO/Supervisionado).

## 🛠️ Tecnologias e Bibliotecas Utilizadas

*   `Python 3`
*   `pandas` & `numpy` (Manipulação, agrupamento e cálculos matemáticos)
*   `scipy.stats` (Módulo `chi2_contingency` para testes de hipótese)
*   `PySUS` (Conexão e download de dados do SINAN)
*   `openpyxl` (Exportação e escrita de dados para Excel)

## 🚀 Como Utilizar

### 1. Pré-requisitos
O código foi concebido visando a execução no **Google Colab** (utilizando o diretório `/content/`). Para rodar em ambiente local ou na nuvem, instale as dependências:

```bash
pip install pysus
pip install --upgrade openpyxl pandas numpy scipy
```

### 2. Execução
Execute as células sequencialmente. O script irá:
1. Baixar os dados dos anos especificados e concatená-los em um único *DataFrame*.
2. Realizar a categorização e tipagem (ex: agrupar idades em faixas etárias).
3. Rodar a função iterativa `funcao()` que computa o OR, p-value e $\chi^2$ para cada variável.
4. Salvar os resultados temporariamente no diretório local.
5. Executar o bloco de compressão (`zipfile`) gerando o arquivo final para download.

## 📁 Estrutura de Diretórios Gerada (Runtime)

Durante a execução, o script alocará os recursos no seguinte formato:

```text
/content/
│
├── TUB_CN/
│   ├── 2019/ TUB_CN_2019.csv
│   ├── 2020/ TUB_CN_2020.csv
│   └── ...
│
├── SEXO_AB.xlsx
├── FAIXA_ETARIA_AB.xlsx
├── DROGAS_AB.xlsx
├── ... (arquivos temporários)
│
└── arquivos_xlsx.zip   (Output Final Consolidado para Download)
```
*(Nota: O script inclui uma rotina de limpeza que apaga as planilhas soltas após a criação do arquivo ZIP, mantendo o ambiente organizado).*
