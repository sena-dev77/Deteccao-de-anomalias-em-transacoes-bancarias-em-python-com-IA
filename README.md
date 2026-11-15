# Link para notebook no Google Colab

[Clique aqui para abrir o notebook completo no Google Colab](https://colab.research.google.com/drive/1ELA-FhfgCxgGLBAky7XIJ1RJoCoc_b0K?usp=sharing)

# Comparativo de Atualizações do Modelo: Código Original vs. Notebook Atualizado

Este documento apresenta as principais melhorias, correções metodológicas e novas abordagens implementadas no notebook de análise de fraudes em relação ao notebook original de aprendizado, disponibilizado pela plataforma de estudos **DIO**, no curso **Santander - Dados com Python e IA**.

---

## 🛠️ Mudanças Principais (Baseadas nas Notas do Notebook Original)

No final do notebook original disponibilizado pela DIO, foram elencadas três modificações fundamentais que direcionaram a atualização para a aula:

1. **Mudança na ordem dos códigos e etapas:** Reestruturação lógica e cronológica do pipeline.
2. **Adição do GridSearchCV no pipeline:** Automatização da otimização de hiperparâmetros com validação cruzada.
3. **Uso de balanceamento (`class_weight="balanced"`/`scale_pos_weight`) no pipeline:** Tratamento do desbalanceamento severo das classes de forma integrada.

---

## 🚀 Outras Atualizações Notáveis e Boas Práticas Adicionadas

Além das mudanças solicitadas originalmente, implementamos melhorias de engenharia de software e ciência de dados críticas:

### 1. Prevenção de Vazamento de Dados (*Data Leakage*)

* **No original (notebook de aprendizado da DIO):** A padronização com `StandardScaler` era realizada no dataset completo antes da divisão em treino e teste (`train_test_split`). Isso permitia que informações estatísticas do conjunto de teste vazassem para o treinamento.
* **No atualizado:** O `StandardScaler` agora é ajustado (`fit_transform`) apenas nas variáveis de treino e aplicado (`transform`) nas de teste, garantindo a integridade da avaliação do modelo.

### 2. Criação Integrada de Pipelines (`sklearn.pipeline.Pipeline`)

* **No original:** As etapas de escala, engenharia e modelagem eram dispersas.
* **No atualizado:** Foi estruturado um pipeline robusto com `Pipeline` e `GridSearchCV` para a Regressão Logística, facilitando a portabilidade, reprodutibilidade e a busca automática pelos melhores hiperparâmetros (como o parâmetro de regularização `C`).

### 3. Ajuste Fino de Threshold (Limiar de Decisão)

* **Otimização de Recall:** O ponto de corte padrão de probabilidade (0.5) foi ajustado para **0.3**, priorizando a sensibilidade do modelo. Isso elevou o Recall de **0.61 para 0.73**, identificando significativamente mais fraudes à custa de uma pequena perda aceitável em precisão.

### 4. Implementação de Random Forest com Balanceamento

* Inclusão do modelo `RandomForestClassifier` com o parâmetro `class_weight="balanced"`, gerando ótimos resultados para lidar com a escassez de dados da classe positiva (fraudes).

### 5. Atualização e Otimização do XGBoost

* Remoção de parâmetros obsoletos como `use_label_encoder=False` (que causavam avisos de deprecação do framework).
* Correção do fluxo de treino com o algoritmo otimizado de Gradient Boosting.

### 6. Explicabilidade do Modelo com SHAP

* Adicionada a biblioteca `SHAP` com amostragem controlada de teste (`X_test[:100]`) para renderizar gráficos de barras de impacto de atributos (`shap.plots.bar`) sem estourar o uso de memória do servidor.

### 6. Explicabilidade do Modelo com SHAP
* Adicionada a biblioteca `SHAP` com amostragem controlada de teste (`X_test[:100]`) para renderizar gráficos de barras de impacto de atributos (`shap.plots.bar`) sem estourar o uso de memória do servidor.
"""
