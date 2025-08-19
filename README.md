# 📊 TelecomX Previsão de Churn de Clientes

## Visão Geral

O projeto **TelecomX Previsão de Churn de Clientes** aborda o desafio de prever a evasão de clientes para uma empresa de telecomunicações. O objetivo é identificar clientes com alta probabilidade de cancelar seus serviços e fornecer insights acionáveis para melhorar as estratégias de retenção. Utilizando um conjunto de dados com informações de clientes, desenvolvemos um pipeline de machine learning para pré-processamento de dados, treinamento de modelos preditivos, avaliação de desempenho e interpretação dos principais fatores que influenciam o churn.

O projeto atende aos seguintes objetivos:
- **Preparação de Dados**: Limpeza, codificação e balanceamento do conjunto de dados para modelagem.
- **Análise de Correlação e Seleção de Variáveis**: Identificação de características relevantes para a previsão de churn.
- **Treinamento de Modelos**: Construção e comparação de múltiplos modelos de classificação.
- **Avaliação de Desempenho**: Análise do desempenho dos modelos com métricas apropriadas.
- **Importância das Variáveis**: Interpretação dos principais drivers de churn.
- **Insights Estratégicos**: Proposta de estratégias baseadas em dados para retenção de clientes.

## Estrutura do Projeto

```
TelecomX_BR_Parte2/
├── TelecomX_br_2.ipynb        # Notebook Jupyter principal com o pipeline de análise
├── dados_tratados.csv        # Conjunto de dados pré-processado (não incluído no repositório)
├── README.md                 # Documentação do projeto
```

## Conjunto de Dados

O conjunto de dados (`dados_tratados.csv`) contém **7.043 registros** e **23 colunas**, incluindo:
- **Variável Alvo**: `Churn` (0 = cliente retido, 1 = cliente evadido)
- **Principais Variáveis**: `tenure`, `Charges.Monthly`, `Charges.Total`, `Contract`, `InternetService`, `OnlineSecurity`, `PaymentMethod`, entre outras.
- **Características dos Dados**:
  - Nenhum valor ausente.
  - Mistura de variáveis numéricas (ex.: `tenure`, `Charges.Monthly`) e categóricas (ex.: `Contract`, `InternetService`).
  - Variável alvo desbalanceada, tratada com SMOTE para oversampling.

## Metodologia

### 1. Pré-processamento de Dados
- **Limpeza**: Verificação de ausência de valores nulos ou em branco.
- **Codificação**: Aplicação de OneHotEncoder para variáveis categóricas (ex.: `Contract`, `InternetService`).
- **Balanceamento**: Uso de SMOTE para corrigir o desequilíbrio na variável `Churn`.

### 2. Seleção de Variáveis e Análise de Correlação
- Análise de correlações para identificar variáveis fortemente associadas ao churn.
- Variáveis como `tenure`, `Charges.Monthly` e `Contract_Month-to-month` foram priorizadas com base em pontuações de importância dos modelos.

### 3. Treinamento de Modelos
- **Divisão dos Dados**: Separação em conjuntos de treino e teste com `train_test_split`.
Três modelos de classificação foram treinados:
- **Regressão Logística**: Modelo linear para entender a direção do impacto das variáveis.
- **Random Forest**: Modelo de ensemble para capturar relações não lineares e importância das variáveis.
- **Máquina de Vetores de Suporte (SVM)**: Modelo não linear com kernel RBF, avaliado com importância por permutação.

### 4. Avaliação dos Modelos
- Os modelos foram avaliados usando métricas como acurácia, precisão, recall e F1-score com `classification_report`.
- A importância das variáveis foi visualizada para cada modelo, identificando os principais drivers de churn.

<img width="985" height="590" alt="image" src="https://github.com/user-attachments/assets/a3bf2996-0389-4afc-9edf-e4b9c7d39984" />

### 5. Análise de Importância das Variáveis
- **Regressão Logística**: Destacou coeficientes (positivos/negativos) para variáveis como `Contract_Month-to-month` (+ve) e `tenure` (-ve).
- **Random Forest**: Classificou variáveis por importância, com `tenure` e `Charges.Monthly` no topo.
- **SVM**: Usou importância por permutação, confirmando `tenure`, `Charges.Monthly` e `Contract_Month-to-month` como críticos.

### 6. Visualização
- Gráficos de barras foram gerados para visualizar a importância das variáveis em cada modelo, facilitando a identificação dos principais preditores de churn.

## Resultados

### Principais Descobertas
As seguintes variáveis foram consistentemente identificadas como as mais influentes em todos os modelos:
- **Tenure**: Clientes com menor tempo de contrato (0-9 meses) têm maior probabilidade de churn.
- **Charges.Monthly**: Custos mensais elevados aumentam a probabilidade de churn.
- **Contract_Month-to-month**: Contratos flexíveis mês a mês estão associados a taxas mais altas de churn.
- **InternetService_Fiber optic**: Clientes com serviços de fibra óptica apresentam maior churn, possivelmente devido a custos ou problemas de serviço.
- **OnlineSecurity_No**: A ausência de serviços de segurança online aumenta a probabilidade de churn.

### Comparação dos Modelos
- **Regressão Logística**: Fornece coeficientes interpretáveis, mostrando a direção do impacto (ex.: contratos mês a mês aumentam o churn).
- **Random Forest**: Altamente discriminativo, priorizando variáveis como `tenure` e `Charges.Monthly`.
- **SVM**: Captura relações não lineares complexas, reforçando a importância de `tenure` e `Contract_Month-to-month`.

## Estratégias de Retenção

Com base na análise, as seguintes estratégias são recomendadas:
1. **Fidelizar Clientes Novos (`tenure`)**: Oferecer programas de fidelidade ou descontos para clientes nos primeiros 12 meses.
2. **Reduzir Custos Mensais (`Charges.Monthly`)**: Introduzir preços escalonados ou descontos para clientes com contas altas.
3. **Incentivar Contratos de Longo Prazo (`Contract_Month-to-month`)**: Oferecer descontos significativos para contratos de 1 ou 2 anos e incentivos para renovação.
4. **Melhorar a Experiência com Fibra Óptica (`InternetService_Fiber optic`)**: Realizar pesquisas de satisfação e oferecer suporte prioritário para clientes de fibra óptica.
5. **Promover Serviços Adicionais (`OnlineSecurity_No`)**: Incluir segurança online gratuita por um período inicial ou em pacotes promocionais.

## Instalação e Uso

1. Clone o repositório:
   ```bash
   git clone https://github.com/IsisVct/TelecomX_BR_Parte2.git
   cd TelecomX_BR_Parte2
   ```

2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

3. Execute o notebook:
   - Abra o arquivo `TelecomX_br_2.ipynb` em um ambiente Jupyter (como Jupyter Notebook ou Google Colab).
   - Certifique-se de ter o arquivo `dados_tratados.csv` no diretório correto ou ajuste o caminho no notebook.

4. Explore os resultados:
   - Execute as células do notebook para visualizar os gráficos de importância das variáveis e os relatórios de desempenho dos modelos.

## Dependências

As dependências estão listadas no arquivo `requirements.txt`. Principais bibliotecas:
- Python 3.8+
- pandas
- numpy
- scikit-learn
- imblearn
- matplotlib
- seaborn


Autor: Isabelle Souza
