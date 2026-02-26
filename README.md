# 🎓 Previsão de Churn Acadêmico: Arquitetura de Pipelines End-to-End

Este projeto vai além do modelo tradicional em Jupyter Notebook. O foco aqui é a construção de uma **solução de Data Science robusta e pronta para produção**, focada na retenção de alunos no ensino superior.

O objetivo principal é identificar precocemente alunos com propensão à evasão (churn) utilizando técnicas de Engenharia de Processo para garantir que o modelo seja escalável e livre de erros comuns, como o *data leakage*.

## 🚀 Diferenciais do Projeto

* **Arquitetura de Pipelines (`scikit-learn`):** Todo o pré-processamento (imputação de nulos, encodings categóricos e normalização) está encapsulado junto ao modelo. Isso garante que os dados de treino e produção passem exatamente pelas mesmas transformações.
* **Prevenção de Data Leakage:** Estruturação rigorosa do fluxo de dados para garantir a integridade da validação.
* **Feature Engineering Customizada:** Implementação de transformadores personalizados (como o `BinarizadorSimNao`) integrados ao `ColumnTransformer`.
* **Foco no Negócio:** Além da métrica técnica ($F_1$-Score e AUC-ROC), o projeto entrega uma **estratégia de ação** baseada em probabilidades, classificando os alunos em:
* 🔴 **Ação Imediata:** Alunos com altíssima probabilidade de evasão.
* 🟡 **Acompanhar:** Alunos em zona de risco moderado.
* 🟢 **Propensão de Sucesso:** Alunos com perfil de graduação.



## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python 3.x
* **Manipulação de Dados:** `Pandas`, `NumPy`
* **Machine Learning:** `Scikit-Learn`, `CatBoostEncoder` (category_encoders)
* **Modelos Avaliados:** Random Forest e K-Nearest Neighbors (KNN)
* **Visualização:** `Matplotlib`, `Seaborn`
* **Persistência:** `Pickle` para exportação da pipeline final.

## 📊 Pipeline de Processamento

A pipeline automática realiza:

1. **Binarização:** Converte variáveis "Sim/Não" para 0/1.
2. **Imputação:** Trata valores ausentes usando a moda (most frequent).
3. **Scaling:** Normalização via `MinMaxScaler` para variáveis numéricas.
4. **Encoding:** Aplicação de `CatBoostEncoder` para variáveis categóricas de alta cardinalidade, capturando a relação com o target sem inflar a dimensionalidade.

## 📈 Resultados

O modelo **Random Forest** apresentou o melhor desempenho, com um **$F_1$-Score médio de 0.89** na validação cruzada, demonstrando excelente capacidade de generalização e equilíbrio entre precisão e sensibilidade (recall).

---

### 📂 Como utilizar

O arquivo `pipeline_rf_final.pkl` contém o objeto completo. Para realizar novas predições, basta carregar o arquivo e chamar o método `.predict()` diretamente nos dados brutos.

```python
import pickle
with open("pipeline_rf_final.pkl", "rb") as f:
    model = pickle.load(f)
    
# O modelo já sabe tratar os dados sozinho!
predicoes = model.predict(novos_dados_brutos)

```

