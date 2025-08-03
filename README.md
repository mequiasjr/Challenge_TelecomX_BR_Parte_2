# Telecom X - Parte 2: Prevendo Churn

## Propósito da Análise
Este projeto desenvolveu modelos preditivos para prever a evasão de clientes (Churn) na Telecom X, utilizando dados tratados da Parte 1. O objetivo foi identificar clientes com maior risco de evasão, determinar as variáveis mais influentes (como `Tenure`, `MonthlyCharges`, e `Contract`) e propor estratégias de retenção. Foram utilizados Regressão Logística e Random Forest, com análises detalhando fatores de churn e recomendações estratégicas.

## Estrutura do Projeto e Organização dos Arquivos
- **TelecomX_BR_P2.ipynb**: Notebook com extração, transformação, modelagem, avaliação e relatório final.
- **dados_tratados.csv**: Arquivo CSV com dados tratados da Parte 1, contendo colunas como `Gender`, `SeniorCitizen`, `Tenure`, `MonthlyCharges`, `TotalCharges`, `DailyCharges`, `Churn`, entre outras.
- **TelecomX_dicionario.md**: Dicionário de dados com descrição das colunas.
- **TelecomX_Data.json**: Dados brutos originais (usados na Parte 1 para gerar `dados_tratados.csv`).

## Preparação dos Dados
- **Classificação das Variáveis**:
  - **Categóricas**: `Gender`, `SeniorCitizen`, `Partner`, `Dependents`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`, `Contract`, `PaperlessBilling`, `PaymentMethod`.
  - **Numéricas**: `Tenure`, `MonthlyCharges`, `TotalCharges`, `DailyCharges`.
  - **Target**: `Churn` (0 = Não, 1 = Sim).
- **Codificação**: Variáveis categóricas não binárias (`Gender`, `InternetService`, `Contract`, `PaymentMethod`) receberam one-hot encoding. Variáveis binárias já estavam codificadas (0/1) da Parte 1.
- **Imputação**: Valores NaN em colunas numéricas foram imputados com a mediana usando `SimpleImputer` para garantir compatibilidade com SMOTE.
- **Normalização**: Variáveis numéricas foram normalizadas com `StandardScaler` para a Regressão Logística, mas não para o Random Forest.
- **Balanceamento**: Verificado desequilíbrio em `Churn` (taxa calculada dinamicamente). SMOTE foi aplicado, se necessário, para balancear classes.
- **Separação**: Dados divididos em 80% treino e 20% teste.
- **Justificativas**:
  - **Regressão Logística**: Escolhida por sua interpretabilidade e eficácia em problemas binários, requerendo normalização devido à sensibilidade à escala.
  - **Random Forest**: Escolhido por capturar relações não lineares, robusto a desequilíbrios e sem necessidade de normalização.
  - **SMOTE**: Aplicado para mitigar viés em classes desequilibradas, melhorando o recall.
  - **Imputação**: Usada mediana para imputar NaNs, garantindo robustez em dados financeiros potencialmente enviesados.

## Exemplos de Gráficos e Insights
- **Distribuição de Evasão**: Gráfico de barras mostrando a taxa de churn. **Insight**: A proporção de churn indica se há desequilíbrio de classes.
- **Matriz de Correlação**: Heatmap destacando forte correlação negativa de `Tenure` e positiva de `MonthlyCharges` com `Churn`. **Insight**: Clientes novos e com altas mensalidades são mais propensos a churn.
- **Boxplot Tenure vs. Churn**: Menor `Tenure` associado a maior churn. **Insight**: Clientes recentes são um grupo de risco.
- **Boxplot TotalCharges vs. Churn**: Menores gastos totais ligados a maior churn. **Insight**: Menor engajamento financeiro aumenta a evasão.
- **Importância das Variáveis (Random Forest)**: Gráfico de barras destacando `Tenure`, `MonthlyCharges`, e `Contract_Month-to-month`. **Insight**: Contratos mensais e custos altos são fatores críticos.
- **Matriz de Confusão**: Visualizações para ambos os modelos, com Random Forest geralmente apresentando melhor recall. **Insight**: Random Forest é mais eficaz em identificar casos de churn.

## Instruções para Executar o Notebook
1. Crie um novo repositório no GitHub (não use o repositório da Parte 1).
2. Faça upload do `TelecomX_BR_P2.ipynb` e do `dados_tratados.csv` no Google Colab.
3. Execute a célula inicial para instalar dependências:
   ```bash
   !pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
   ```
4. Execute todas as células sequencialmente. O notebook inclui:
   - Carregamento de `dados_tratados.csv` (ou recriação a partir da API, se necessário).
   - Transformação (codificação, imputação, balanceamento, normalização).
   - Modelagem (Regressão Logística e Random Forest).
   - Avaliação com métricas (acurácia, precisão, recall, F1-score, matriz de confusão).
   - Análise de importância das variáveis.
   - Relatório final com insights e recomendações.
5. Certifique-se de que `dados_tratados.csv` está em `/content/` ou execute a célula de recriação.

**Notas**:
- **Dependências**: Python 3.8+ e bibliotecas listadas.
- **Possíveis Problemas**: Se `dados_tratados.csv` não estiver disponível, a célula de recriação usa a API para gerá-lo. Valores NaN são imputados com a mediana para garantir compatibilidade com SMOTE.
