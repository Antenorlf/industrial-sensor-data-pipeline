# 🏭 Pipeline de Dados para Sensores Industriais e Manutenção Preditiva

> Pipeline completo de Engenharia de Dados e Machine Learning para transformar sinais brutos de sensores industriais em um dataset analítico pronto para aplicações de Inteligência Artificial.

---

# 📖 Sobre o Projeto

Em ambientes industriais, equipamentos como sistemas hidráulicos geram continuamente milhares de medições provenientes de sensores de pressão, temperatura, vazão, potência e eficiência.

Entretanto, esses dados normalmente são disponibilizados em arquivos brutos e distribuídos entre diversos sensores, dificultando sua utilização em modelos analíticos.

Este projeto tem como objetivo construir um pipeline completo de dados inspirado em arquiteturas utilizadas em ambientes produtivos, transformando sinais brutos em um conjunto de dados estruturado para aplicações de Machine Learning voltadas à manutenção preditiva.

O projeto foi desenvolvido utilizando **Apache Spark**, **Delta Lake**, **Databricks** e **Python**, seguindo a arquitetura **Medallion (Bronze → Silver → Gold)**.

---

# 🎯 Objetivos

- Construir uma pipeline completa de dados para sensores industriais;
- Organizar dados utilizando a arquitetura Bronze, Silver e Gold;
- Aplicar Engenharia de Features em séries temporais;
- Consolidar múltiplos sensores em um único dataset analítico;
- Disponibilizar uma base preparada para diferentes modelos de Machine Learning;
- Demonstrar um fluxo semelhante ao utilizado em projetos industriais.

---

# 🏭 Dataset

O projeto utiliza o conjunto de dados **Condition Monitoring of Hydraulic Systems**, disponível na UCI Machine Learning Repository.

O sistema hidráulico monitorado possui sensores responsáveis por medir diferentes variáveis físicas durante cada ciclo de operação da máquina.

### Sensores utilizados

- CE
- CP
- EPS1
- FS1
- FS2
- PS1
- PS2
- PS3
- PS4
- PS5
- PS6
- SE
- TS1
- TS2
- TS3
- TS4
- VS1

Cada sensor registra centenas ou milhares de medições para cada ciclo operacional.

---

# 🏗 Arquitetura

```text
Arquivos TXT (Sensores)

        │
        ▼

Bronze (Delta Lake)
Ingestão dos dados brutos

        │
        ▼

Silver
Feature Engineering

        │
        ▼

Gold
Dataset Analítico

        │
        ▼

Machine Learning

        │
        ▼

Predição das Condições dos Componentes
```

---

# ⚙️ Tecnologias Utilizadas

- Python
- Apache Spark
- PySpark
- Databricks
- Delta Lake
- Pandas UDF
- Pandas
- NumPy
- Scikit-Learn
- XGBoost

---


```

---

# 🥉 Camada Bronze

Responsável pela ingestão dos arquivos brutos dos sensores.

Nesta etapa são realizadas:

- Leitura dos arquivos TXT;
- Organização por sensor;
- Identificação dos ciclos de operação;
- Armazenamento em formato Delta Lake.

O objetivo da Bronze é preservar os dados exatamente como foram recebidos.

---

# 🥈 Camada Silver

Na camada Silver ocorre a Engenharia de Features.

Cada ciclo operacional é convertido em um conjunto de atributos estatísticos que representam o comportamento do sensor.

Para cada sensor foram extraídas as seguintes características:

| Feature | Descrição |
|----------|-----------|
| Mean | Média |
| Standard Deviation | Desvio padrão |
| Minimum | Valor mínimo |
| Maximum | Valor máximo |
| Median | Mediana |
| Range | Amplitude |
| RMS | Root Mean Square |
| Skewness | Assimetria |
| Kurtosis | Curtose |
| Slope | Tendência do sinal |

A extração foi implementada utilizando **Pandas UDF**, permitindo processamento distribuído com Apache Spark.

---

# 🥇 Camada Gold

Na camada Gold todas as features geradas são consolidadas em um único dataset.

Cada linha representa um ciclo completo da máquina.

Cada coluna representa uma característica estatística extraída de um sensor.

Além das features, o dataset contém os rótulos utilizados para classificação dos componentes hidráulicos.

Essa estrutura torna a base reutilizável para diferentes algoritmos de Machine Learning.

---

# 🤖 Machine Learning

Como prova de conceito, foi utilizado o algoritmo **XGBoost** para classificação das condições do componente **Cooler**.

Fluxo utilizado:

```text
Dataset Gold

↓

Separação Treino/Teste

↓

XGBoost

↓

Validação Cruzada

↓

Análise de Importância das Features
```

---

# 📈 Resultados

Utilizando **Stratified K-Fold Cross Validation**, o modelo apresentou desempenho consistente durante os experimentos.

Além da avaliação do modelo, também foi realizada análise da importância das features, permitindo identificar quais sensores mais contribuíram para a classificação.

Mais importante do que o desempenho obtido foi demonstrar que um pipeline estruturado de Engenharia de Dados fornece uma base sólida para aplicações de Inteligência Artificial.

---

# 💡 Principais Aprendizados

Durante o desenvolvimento deste projeto, ficou evidente que o maior desafio não está no treinamento do modelo de Machine Learning.

Grande parte do esforço está relacionada à organização dos dados, engenharia de atributos e construção de uma pipeline confiável.

Essa é uma realidade comum em projetos industriais, onde a qualidade dos dados costuma impactar diretamente o desempenho dos modelos analíticos.

---

# 🚀 Próximos Passos

- Comparação entre XGBoost, LightGBM e CatBoost;
- Novas técnicas de Feature Engineering para séries temporais;
- Otimização automática de hiperparâmetros;
- Versionamento de modelos com MLflow;
- Criação de uma API para inferência;
- Dashboard para monitoramento dos sensores;
- Evolução para um pipeline de MLOps.

---



---

# 👨‍💻 Autor

**Antenor Lorenção Ferreira**

🔗 LinkedIn:
https://www.linkedin.com/in/antenor-lorencao-866116292

---

## ⭐ Se este projeto foi útil ou interessante, considere deixar uma estrela no repositório.
