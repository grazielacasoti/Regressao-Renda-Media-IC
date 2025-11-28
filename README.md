# Projeto Final: Regressão da Renda Média no Brasil (2013-2023)

## Introdução e Resumo do Problema

Este projeto de **Inteligência Computacional** foca na aplicação de técnicas de Machine Learning para resolver um problema de **Regressão**.

O objetivo principal é construir um modelo preditivo capaz de estimar a Renda Média (`Renda_Media`) em diferentes contextos geográficos e administrativos no Brasil e a relação com a Evasão Escolar.

O *dataset* utilizado, `AbandonoEscolar_RendaMedia_2013_2023.csv`, contém variáveis cruciais como a `Taxa_Abandono` e informações regionais e administrativas, permitindo analisar a correlação entre fatores educacionais e a distribuição de renda ao longo dos anos.

---

## Solução e Modelagem

### 2.1. Pipeline de Pré-processamento

Para garantir a qualidade dos dados e prepará-los para a modelagem, foi implementado um `ColumnTransformer` (Pipeline) com as seguintes etapas:

1.  **Imputação:** Tratamento de valores ausentes (`NaN`) na coluna numérica `Taxa_Abandono` com a mediana.
2.  **Escalonamento:** Normalização das *features* numéricas (`Ano`, `Taxa_Abandono`) utilizando o `StandardScaler`.
3.  **Codificação:** Transformação de variáveis categóricas (`Regiao`, `Localizacao`, etc.) em formato numérico utilizando o `OneHotEncoder`.

### Modelos Avaliados e Ajuste Fino

Foram treinados e avaliados três modelos de Regressão via Validação Cruzada (`cv=5`) no conjunto de treino:

| Modelo | RMSE Médio (CV) |
| :--- | :--- |
| **Linear Regression** (Baseline) | R$ 125.55] |
| **Decision Tree Regressor** | R$ [0.33] |
| **Random Forest Regressor** | R$ [0.80] |

O **Random Forest Regressor** demonstrou o melhor desempenho inicial e foi escolhido para o Ajuste Fino de hiperparâmetros. Foi utilizado o **`[GridSearchCV ou RandomizedSearchCV]`** para otimizar os parâmetros.

## Resultados e Avaliação

O modelo final, treinado com os hiperparâmetros otimizados, foi avaliado no conjunto de **Teste** (dados não vistos), garantindo uma avaliação real do seu desempenho.

| Métrica | Valor Final no Teste | Interpretação |
| :--- | :--- | :--- |
| **RMSE (Root Mean Squared Error)** | **R$ [99.99]** | O erro médio de previsão do modelo em Reais. |
| **R² (Coeficiente de Determinação)** | **[0.9769]%** | Porcentagem da variância da Renda Média explicada pelas *features*. |

### Análise:

O modelo obteve um **$R^2$ de [0.9769]%**, indicando que a grande maioria da variação na Renda Média é capturada pelas variáveis em análise. O **RMSE de R$ [99.99]** é considerado Excelente dado que a média da `Renda_Media` no *dataset* é de R$ [2637.198447].

---

## Discussões e Interpretação

### Importância das Variáveis (*Feature Importance*)

Principais fatores de influência na Evasão Escolar além da Renda Média:

Ano
O modelo aprende que a renda média aumenta (nominalmente) com o passar dos anos. O ano é um indicador direto da evolução econômica.

Taxa_Abandono Capital
Indicador do nível educacional e de desenvolvimento humano da população. Menor abandono implica maior escolaridade, maior produtividade e, consequentemente, salários e rendas mais elevadas.

Regiao_X
O modelo mostra as desigualdades estruturais do Brasil. Regiões mais industrializadas e com maior concentração de serviços (como o Sudeste e o Sul) possuem salários e rendas médias consistentemente mais altas.

Dependencia_Administrativa_Privada
A renda média associada a escolas privadas ou federais (onde a taxa de abandono é tipicamente muito baixa) reflete a população com maior poder aquisitivo ou que acessa instituições de alto padrão.

### O Porquê da Influência:

O atributo `Taxa_Abandono` demonstrou ser um dos mais importantes, confirmando a forte correlação negativa entre indicadores educacionais e renda. Quanto menor a taxa de abandono (indicando maior capital humano), maior tende a ser a Renda Média da região. O Ano` também é crucial, atuando como um *proxy* para o crescimento econômico e a inflação nominal ao longo do tempo. Variáveis geográficas (como `Regiao`) refletem as disparidades econômicas estruturais do Brasil.

---

## Trabalhos Futuros

Para aprimorar a solução, trabalhos futuros podem seguir os seguintes caminhos:

1. Implementar um tratamento explícito de *outliers* (ex: IQR ou Isolation Forest) na `Taxa_Abandono` para verificar se isso melhora a estabilidade do modelo.
2. Realizar melhorias no Randomized Search, aprimorando o modelo e diminuindo o tempo de execução da máquina.
3. Busca de novos Datasets de correlação entre Renda Média e Evasão Escolar com novas variáveis de influência.
4.  **Engenharia de Features:** Criar novas *features* de interação (ex: `Taxa_Abandono` $\times$ `Localizacao_Rural`).
5.  **Modelos Avançados:** Testar algoritmos de *Boosting*, como **XGBoost** ou **LightGBM**, que são conhecidos por oferecerem desempenho superior em problemas de regressão tabular.

#Adicionando documentação inicial da Atividade Final 
