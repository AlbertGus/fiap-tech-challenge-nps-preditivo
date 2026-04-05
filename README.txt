# Tech Challenge Fase 1 - FIAP | Modelo Preditivo de NPS para E-commerce

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Machine_Learning-Scikit_Learn-orange)](https://scikit-learn.org/)
[![Status](https://img.shields.io/badge/Status-Concluído-success)]()

## 📌 Objetivo do Projeto
Este projeto foi desenvolvido como requisito de avaliação da Fase 1 da pós-graduação. O objetivo central é resolver a dor de negócio de um e-commerce que sofre com a reatividade na medição da experiência do consumidor. Atualmente, o Net Promoter Score (NPS) é mensurado apenas no encerramento da jornada, limitando a capacidade da empresa de antecipar problemas. 

A proposta deste repositório é realizar uma **mudança de paradigma de reativo para preditivo**, utilizando Ciência de Dados para identificar os fatores operacionais críticos e treinar um modelo de Inteligência Artificial capaz de classificar o sentimento do cliente (Detrator, Neutro ou Promotor) antes do envio da pesquisa, permitindo atuação proativa da equipe de *Customer Experience* (CX).

## 🗂️ Descrição da Base de Dados
A base de dados utilizada reflete a operação logística e de atendimento de um e-commerce, contendo 2.500 registros únicos de clientes sem valores nulos. 

**Principais variáveis utilizadas:**
* **Demográficas/Perfil:** `customer_age` (idade), `customer_region` (região), `customer_tenure_months` (tempo de relacionamento).
* **Transacionais:** `order_value` (valor do pedido), `repeat_purchase_30d` (recompra nos últimos 30 dias).
* **Operacionais (Alavancas de NPS):** `delivery_delay_days` (dias de atraso na entrega), `customer_service_contacts` (volume de acionamentos do suporte).
* **Variável Alvo:** A coluna original contínua `nps_score` (0 a 10) foi transformada na variável categórica `nps_class` (Detrator, Neutro, Promotor) para adequação ao modelo preditivo.
* *Nota:* Variáveis de pós-venda (como notas internas de CSAT e contagem de reclamações) foram removidas para evitar *Data Leakage* (fuga de dados).

## 🧠 Metodologia Utilizada
O projeto foi dividido em duas grandes etapas, refletidas na organização dos notebooks:

**1. Análise Exploratória de Dados (EDA) com Foco em Negócio:**
* Utilização de Matriz de Correlação para identificar que os atrasos logísticos e o atrito no atendimento são os maiores ofensores da satisfação.
* Identificação de "Pontos de Ruptura": Foi comprovado que a partir de **2.5 dias de atraso**, a quebra de expectativa é severa e o cliente se torna um detrator (e interrompe a recompra, gerando *Churn* imediato).

**2. Modelagem Preditiva (Machine Learning):**
* **Abordagem:** Classificação (ao invés de Regressão) por ser mais acionável para o negócio.
* **Algoritmo:** `RandomForestClassifier`.
* **Transformações:** Aplicação de *One-Hot Encoding* (Dummies) para variáveis categóricas de região.
* **Avaliação e Robustez:** O modelo foi avaliado com foco na métrica de **Recall** para a classe "Detrator", atingindo impressionantes **99%** de captura. Para garantir a ausência de *overfitting*, aplicou-se a técnica de *K-Fold Cross-Validation* (cv=5), que retornou uma acurácia média real de 82% com um desvio padrão baixíssimo de 0.009.

## 📁 Estrutura de Pastas
O repositório está organizado utilizando as melhores práticas de estruturação de projetos de dados:
* `data/`: Contém o dataset original em formato `.csv`.
* `notebooks/`: Códigos modulares, comentados e divididos cronologicamente (`01_exploracao_e_preparacao.ipynb` e `02_modelagem_preditiva.ipynb`).
* `docs/`: Documentação de negócio, incluindo o Sumário Executivo em PDF e a documentação técnica do desafio.

## 🚀 Como Reproduzir os Resultados
Para garantir a reprodutibilidade desta análise por qualquer pessoa ou avaliador:
1. Faça o clone deste repositório ou o download dos arquivos em formato ZIP.
2. Certifique-se de ter um ambiente Python 3.8+ instalado (recomenda-se a distribuição Anaconda).
3. Instale as dependências listadas executando no terminal: `pip install pandas numpy matplotlib seaborn scikit-learn`
4. Abra o ambiente Jupyter Notebook e execute as células sequencialmente, começando pelo notebook `01_exploracao_e_preparacao.ipynb` (que gerará a base limpa) e, em seguida, o `02_modelagem_preditiva.ipynb`.
