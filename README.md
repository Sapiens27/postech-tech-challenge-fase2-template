# Tech Challenge — Fase 2 | POSTECH Data Analytics

> **INSTRUÇÕES:** este README é um template. Substitua **todos** os blocos marcados com
> `<!-- PREENCHER -->` e apague as linhas de instrução antes de submeter.

---

## 1. Identificação

| Campo | Valor |
|---|---|
| Turma | 2DTATBB |
| Grupo | Individual |
| Data de entrega | 30/09/2026 |

### Integrantes

| Nome completo | RM | E-mail |
|---|---|---|
| Leandro Alexandre da Silva | RM377795 | lads.627@bb.com.br |

---

## 2. Links da entrega

Estes três links são **obrigatórios** e devem ser idênticos aos do PDF de submissão.

| Item | Link |
|---|---|
| Repositório | https://github.com/Sapiens27/postech-tech-challenge-fase2-template |
| Vídeo executivo (≤ 5 min) | <!-- PREENCHER: YouTube não listado / Drive com acesso liberado --> |
| Apresentação | <!-- PREENCHER: link do arquivo em `docs/` ou Drive --> |

> ⚠️ Repositório privado ou inacessível inviabiliza a avaliação da entrega.
> Confira o acesso em uma janela anônima antes de enviar.

---

## 3. O problema

A análise de risco de crédito busca identificar clientes com maior probabilidade de apresentar problemas de pagamento. A capacidade de distinguir perfis de menor e maior risco pode apoiar instituições financeiras na avaliação de crédito e na tomada de decisões mais consistentes.

Neste projeto, técnicas de Machine Learning são utilizadas para analisar características cadastrais, socioeconômicas e profissionais dos clientes e verificar sua capacidade de discriminar clientes que apresentaram ou não atrasos relevantes no histórico de crédito observado.

O problema foi estruturado como uma tarefa de **classificação binária**, na qual o modelo busca distinguir bons e maus pagadores a partir das informações disponíveis nas bases de dados.

### Variável alvo

A variável-alvo `TARGET` foi construída a partir do histórico mensal disponível em `credit_record.csv`.

Foi definido:

- `TARGET = 1`: cliente que apresentou pelo menos uma ocorrência de atraso igual ou superior a 30 dias, correspondente aos valores de `STATUS` entre `1` e `5`;
- `TARGET = 0`: cliente sem ocorrência de atraso igual ou superior a 30 dias no histórico observado.

Após a construção da variável-alvo, foram identificados **36.457 clientes** presentes nas duas bases. Destes, **4.291 (11,77%)** foram classificados como `TARGET = 1` e **32.166 (88,23%)** como `TARGET = 0`.

Essa distribuição evidencia um problema de classes desbalanceadas, considerado tanto na escolha das métricas de avaliação quanto na comparação dos modelos.

### Dataset

| Campo | Valor |
|---|---|
| Fonte | [Kaggle — Credit Card Approval Prediction](https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction/data) |
| Linhas × colunas | `application_record.csv`: 438.557 × 18; `credit_record.csv`: 1.048.575 × 3 |
| Período / versão | Dataset disponibilizado publicamente no Kaggle |
| Licença de uso | CC0: Public Domain |

Descrição das variáveis:

Descrição das variáveis:

| Variável | Tipo | Descrição |
|---|---|---|
| `ID` | Numérica | Identificador único do cliente |
| `CODE_GENDER` | Categórica | Gênero do cliente |
| `FLAG_OWN_CAR` | Categórica | Indica se o cliente possui automóvel |
| `FLAG_OWN_REALTY` | Categórica | Indica se o cliente possui imóvel |
| `CNT_CHILDREN` | Numérica | Número de filhos |
| `AMT_INCOME_TOTAL` | Numérica | Renda total declarada |
| `NAME_INCOME_TYPE` | Categórica | Tipo/origem da renda |
| `NAME_EDUCATION_TYPE` | Categórica | Nível de escolaridade |
| `NAME_FAMILY_STATUS` | Categórica | Estado civil/situação familiar |
| `NAME_HOUSING_TYPE` | Categórica | Tipo de moradia |
| `DAYS_BIRTH` | Numérica | Idade representada em dias antes da transformação |
| `DAYS_EMPLOYED` | Numérica | Tempo de emprego representado em dias antes da transformação |
| `FLAG_MOBIL` | Binária | Indicador de telefone celular |
| `FLAG_WORK_PHONE` | Binária | Indicador de telefone de trabalho |
| `FLAG_PHONE` | Binária | Indicador de telefone |
| `FLAG_EMAIL` | Binária | Indicador de e-mail |
| `OCCUPATION_TYPE` | Categórica | Tipo de ocupação profissional |
| `CNT_FAM_MEMBERS` | Numérica | Número de membros da família |
| `MONTHS_BALANCE` | Numérica | Período mensal relativo do histórico de crédito |
| `STATUS` | Categórica | Situação mensal do crédito/pagamento |
| `TARGET` | Binária derivada | Variável-alvo criada no projeto: 1 para cliente com ao menos um atraso ≥ 30 dias (`STATUS` de 1 a 5); 0 caso contrário |
| `AGE_YEARS` | Numérica derivada | Idade em anos, criada a partir de `DAYS_BIRTH` |
| `YEARS_EMPLOYED` | Numérica derivada | Tempo de emprego em anos, criado a partir de `DAYS_EMPLOYED` |
---

## 4. Como reproduzir

Clone o repositório e acesse a pasta do projeto:

```bash
git clone https://github.com/Sapiens27/postech-tech-challenge-fase2-template.git
cd postech-tech-challenge-fase2-template
```

Crie e ative um ambiente virtual:

```bash
python -m venv .venv
source .venv/bin/activate
# Windows: .venv\Scripts\activate
```

Instale as dependências do projeto:

```bash
pip install -r requirements.txt
```

Inicie o Jupyter Notebook:

```bash
jupyter notebook
```

Os dados utilizados no projeto não são versionados no repositório.

Baixe o dataset **Credit Card Approval Prediction** no Kaggle:

https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction/data

Após o download, coloque os seguintes arquivos na pasta `data/raw/`:

- `application_record.csv`
- `credit_record.csv`

A estrutura esperada é:

```text
data/
└── raw/
    ├── application_record.csv
    └── credit_record.csv
```

Os notebooks utilizam caminhos relativos para acessar esses arquivos, permitindo a reprodução do projeto independentemente do diretório local utilizado.

Execute os notebooks nesta ordem:

1. `notebooks/01_eda.ipynb` — análise exploratória dos dados, construção da variável-alvo e análises estatísticas;
2. `notebooks/02_preprocessamento.ipynb` — limpeza, transformação das variáveis, divisão entre treino e teste e construção do pipeline de pré-processamento;
3. `notebooks/03_modelagem.ipynb` — treinamento, validação cruzada e comparação dos modelos de classificação;
4. `notebooks/04_avaliacao.ipynb` — avaliação final do modelo selecionado no conjunto de teste, análise das métricas, importância das variáveis e conclusões.

A ordem de execução deve ser mantida para acompanhar corretamente as etapas metodológicas desenvolvidas no projeto.
---

## 5. Resultados

| Modelo | Acurácia | Precisão | Recall | F1 | AUC-ROC |
|---|---:|---:|---:|---:|---:|
| Random Forest | 0,89 | 0,54 | 0,32 | 0,40 | 0,805 |

**Modelo escolhido:** Random Forest.

O Random Forest apresentou o melhor desempenho entre os algoritmos avaliados durante a etapa de validação cruzada, superando a Regressão Logística e o HistGradientBoosting. O modelo foi então avaliado uma única vez no conjunto de teste reservado, obtendo AUC-ROC de aproximadamente **0,805**.

**Métricas priorizadas:** devido ao desbalanceamento da variável-alvo — aproximadamente **11,77%** dos clientes pertencem à classe de maus pagadores — a acurácia isoladamente não é suficiente para avaliar a qualidade do modelo. Foram priorizadas métricas capazes de avaliar a discriminação da classe minoritária, especialmente **AUC-ROC, PR-AUC, recall, precisão e F1-score**.

No conjunto de teste, para a classe de maus pagadores (`TARGET = 1`), o modelo apresentou **precisão de 0,54**, **recall de 0,32** e **F1-score de 0,40**. A **PR-AUC foi de aproximadamente 0,424**.

A matriz de confusão apresentou **276 verdadeiros positivos, 582 falsos negativos, 236 falsos positivos e 6.198 verdadeiros negativos**. Esses resultados mostram que, embora o modelo apresente capacidade de discriminação, ainda deixa de identificar uma parcela relevante dos maus pagadores, aspecto especialmente importante em uma aplicação de risco de crédito.
---

## 6. Principais conclusões

1. **O perfil de risco não é explicado por uma única característica.** As análises individuais mostraram associações relativamente fracas entre as variáveis e a inadimplência, enquanto o Random Forest apresentou melhor capacidade de discriminação ao considerar conjuntamente as características dos clientes. Isso reforça a utilidade de uma abordagem multivariada para avaliação de risco.

2. **Idade e tempo de emprego foram as variáveis com maior importância preditiva no modelo**, seguidas pelo tipo de renda, posse de imóvel, ocupação profissional, renda total e escolaridade. Esses resultados indicam que características relacionadas ao momento de vida, estabilidade profissional e situação socioeconômica contribuíram para a classificação realizada pelo modelo.

3. **O modelo apresentou capacidade relevante de separar clientes de diferentes níveis de risco**, alcançando AUC-ROC de aproximadamente 0,805 no conjunto de teste. Entretanto, para a classe de maus pagadores, o recall foi de 0,32, indicando que uma parcela significativa dos clientes que apresentaram atrasos de 30 dias ou mais não foi identificada pelo modelo.

4. **O modelo deve ser utilizado como ferramenta de apoio à decisão, e não como critério isolado para concessão de crédito.** Antes de uma aplicação prática, seria necessário avaliar diferentes limiares de classificação, os custos associados a falsos positivos e falsos negativos e validar o desempenho em dados mais recentes e representativos da população em que o modelo seria utilizado.

### Limitações e próximos passos

O projeto apresenta algumas limitações que devem ser consideradas na interpretação dos resultados. A variável-alvo é desbalanceada, com apenas 11,77% dos clientes classificados como maus pagadores, e sua definição depende do critério adotado de atraso igual ou superior a 30 dias. Além disso, o dataset possui limitações quanto à origem, período e representatividade dos dados, o que impede assumir que o desempenho observado será mantido em outras populações ou períodos.

Como próximos passos, recomenda-se:

- avaliar diferentes limiares de classificação, buscando melhorar a identificação de maus pagadores;
- considerar explicitamente o custo de falsos negativos e falsos positivos na escolha do limiar;
- testar novas técnicas de tratamento do desbalanceamento e outros algoritmos de classificação;
- realizar validação temporal quando houver dados com referência cronológica adequada;
- validar o modelo em dados externos e mais recentes antes de qualquer utilização prática.

Os resultados apresentados devem ser interpretados como **associações preditivas**, e não como relações de causa e efeito entre as características dos clientes e a inadimplência.
---

## 7. Estrutura do repositório

```text
.
├── data/
│   ├── raw/                 dados brutos — não versionados
│   └── processed/           dados processados — não versionados
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessamento.ipynb
│   ├── 03_modelagem.ipynb
│   └── 04_avaliacao.ipynb
├── docs/                    apresentação e documentação da entrega
├── results/                 resultados e artefatos gerados
├── src/                     código-fonte auxiliar
├── submissao/               arquivos relacionados à submissão
├── requirements.txt         dependências do projeto
└── README.md                documentação principal
```

Os dados brutos não são versionados no Git. Para reproduzir o projeto, os arquivos `application_record.csv` e `credit_record.csv` devem ser baixados da fonte indicada e colocados localmente em `data/raw/`.

Os notebooks estão organizados de acordo com a sequência das etapas do projeto, desde a análise exploratória até a avaliação final do modelo.

Detalhes e convenções em [`ESTRUTURA.md`](ESTRUTURA.md).  
Antes de enviar, percorra o [`CHECKLIST.md`](CHECKLIST.md).
---

## 8. Tecnologias

- Python 3
- Jupyter Notebook / Google Colab
- pandas
- NumPy
- Matplotlib
- scikit-learn
- SciPy
- Git e GitHub
