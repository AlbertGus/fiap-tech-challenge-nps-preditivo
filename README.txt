# Tech Challenge Fase 1 - FIAP | Modelo Preditivo de NPS para E-commerce

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Machine_Learning-Scikit_Learn-orange)](https://scikit-learn.org/)
[![Status](https://img.shields.io/badge/Status-Concluído-success)]()

## 🎥 Apresentação do Projeto (Vídeo)
**[Clique aqui para assistir ao vídeo de apresentação do projeto no YouTube](https://youtu.be/bQ7kNFKWmS0) **

## 📌 Objetivo do Projeto
Este projeto foi desenvolvido como requisito de avaliação da Fase 1 da pós-graduação. O objetivo central é resolver a dor de negócio de um e-commerce que sofre com a reatividade na medição da experiência do consumidor. Atualmente, o Net Promoter Score (NPS) é mensurado apenas no encerramento da jornada, limitando a capacidade da empresa de antecipar problemas. 

A proposta deste repositório é realizar uma **mudança de paradigma de reativo para preditivo**, utilizando Ciência de Dados para identificar os fatores operacionais críticos e treinar um modelo de Inteligência Artificial capaz de prever a nota exata do cliente antes do envio da pesquisa. Com essa previsão, classificamos o sentimento (Detrator, Neutro ou Promotor) de forma mais precisa, permitindo uma atuação proativa da equipe de *Customer Experience* (CX).

## 🗂️ Descrição da Base de Dados
A base de dados utilizada reflete a operação logística e de atendimento de um e-commerce, contendo 2.500 registros únicos de clientes sem valores nulos. 

**Principais variáveis utilizadas:**
* **Demográficas/Perfil:** `customer_age` (idade), `customer_region` (região), `customer_tenure_months` (tempo de relacionamento).
* **Transacionais:** `order_value` (valor do pedido), `repeat_purchase_30d` (recompra nos últimos 30 dias).
* **Operacionais (Alavancas de NPS):** `delivery_delay_days` (dias de atraso na entrega), `customer_service_contacts` (volume de acionamentos do suporte).
* **Variável Alvo:** A coluna original contínua `nps_score` (0 a 10) foi **mantida de forma contínua** para o treinamento de um modelo de regressão. 
* *Nota:* Variáveis de pós-venda (como notas internas de CSAT e contagem de reclamações) foram removidas da modelagem para evitar *Data Leakage* (fuga de dados).

## 🧠 Metodologia Utilizada
O projeto foi dividido em duas grandes etapas, refletidas na organização dos notebooks:

**1. Análise Exploratória de Dados (EDA) e Saneamento:**
* Construção de uma **Matriz de Correlação Completa** para identificação de multicolinearidade e validação das variáveis preditoras.
* Foi comprovado estatisticamente que a lealdade prévia (recompra em 30 dias), os atrasos logísticos e o atrito no atendimento (múltiplos contatos) são os maiores ofensores e direcionadores da nota do cliente.

**2. Modelagem Preditiva (Machine Learning):**
* **Abordagem (O Diferencial):** Regressão contínua com posterior categorização de negócio. Em vez de tentar "encaixotar" o cliente (o que gera alto erro na fronteira da classe Neutra), o modelo prevê a nota contínua (ex: 8.2) e a regra de negócio a converte em classe, garantindo altíssima precisão.
* **Algoritmo:** `RandomForestRegressor`.
* **Transformações:** Aplicação de *One-Hot Encoding* (Dummies) para transformar variáveis de texto (região) em numéricas.
* **Avaliação de Performance:** O dataset foi dividido em 80% Treino e 20% Teste para validação. O modelo final obteve um **$R^2$ de 0.62** (provando que 62% da variação da nota é explicada puramente pela operação) e um **MAE (Erro Médio Absoluto) de apenas 1.25 pontos**, demonstrando uma capacidade preditiva de excelência.

## 📁 Estrutura de Pastas
O repositório está organizado utilizando as melhores práticas de estruturação de projetos de dados:
* `data/`: Contém o dataset original em formato `.csv` e a base limpa gerada (`dados_preparados_regressao.csv`).
* `notebooks/`: Códigos modulares, comentados e divididos cronologicamente (`01_exploracao_e_preparacao.ipynb` e `02_modelagem_preditiva.ipynb`).
* `docs/`: Documentação de negócio, incluindo o PDF com as respostas do Tech Challenge e a defesa estratégica.

## 🚀 Como Reproduzir os Resultados
Para garantir a reprodutibilidade desta análise por qualquer pessoa ou avaliador:
1. Faça o clone deste repositório ou o download dos arquivos em formato ZIP.
2. Certifique-se de ter um ambiente Python 3.8+ instalado (recomenda-se a distribuição Anaconda).
3. Instale as dependências executando no terminal: `pip install pandas numpy matplotlib seaborn scikit-learn`
4. Abra o ambiente Jupyter Notebook e execute as células sequencialmente. Comece pelo `01_exploracao_e_preparacao.ipynb` (que gerará a base saneada) e, em seguida, execute o `02_modelagem_preditiva.ipynb`.
