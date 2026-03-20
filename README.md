# FIAP — Tech Challenge / Análise de voos (RM367414)

Projeto de **ciência de dados** sobre o conjunto **`flights.csv`**: exploração dos dados (EDA), **modelo supervisionado** para previsão de atraso na chegada e **modelo não supervisionado** (agrupamento e redução de dimensionalidade). Todo o fluxo está em **notebooks Jupyter**; não há módulos `.py` separados — a lógica de limpeza e features é reutilizada entre notebooks.

---

## Estrutura do repositório

| Item | Descrição |
|------|-----------|
| [`eda_flights.ipynb`](eda_flights.ipynb) | **EDA**: estatísticas descritivas, gráficos (atrasos, cancelamentos, sazonalidade, companhias, aeroportos, horários) e tratamento de ausentes (incluindo campos ligados a `CANCELLED` / `DIVERTED`). |
| [`modelo_classificacao.ipynb`](modelo_classificacao.ipynb) | **Classificação supervisionada**: target *atrasado na chegada* (`ARRIVAL_DELAY` > 15 min), apenas voos não cancelados e não desviados; features **conhecidas antes do voo** (companhia, aeroportos, data, horário programado, distância, tempo programado). Pipelines com `ColumnTransformer` (One-Hot + escalonamento), **Random Forest** e **Regressão Logística**; matriz de confusão, validação cruzada e importância de variáveis. |
| [`modelo_nao_supervisionado.ipynb`](modelo_nao_supervisionado.ipynb) | **Aprendizado não supervisionado**: **K-Means** em perfis de rotas/aeroportos, **PCA** para visualização e análises complementares de atrasos. |
| [`requirements.txt`](requirements.txt) | Dependências Python (`pandas`, `numpy`, `matplotlib`, `seaborn`, `pyarrow`, `scikit-learn`, `jupyterlab`). |
| [`README_EDA.md`](README_EDA.md) | Notas rápidas sobre execução do EDA (com dica de SSL no macOS). |

### Dados

- **`flights.csv`** — base principal de voos (deve ficar na **raiz** do projeto ou em **`data/`**). Por tamanho, costuma estar no `.gitignore`; obtenha o arquivo conforme orientação do curso.
- **`airports.csv`** e **`airlines.csv`** — opcionais para enriquecer o EDA; o notebook procura em `.` ou `data/`.
- Pasta **`data/`** (ignorada pelo Git no `.gitignore` atual) — pode conter **artefatos gerados** pelos notebooks, por exemplo:
  - `pca_voos_2d.csv`
  - `routes_clusters_sample.csv`
  - `routes_clusters_summary.csv`

> **Ordem sugerida:** `eda_flights.ipynb` → `modelo_classificacao.ipynb` → `modelo_nao_supervisionado.ipynb`.

---

## Ambiente e execução

Requisitos: **Python 3.9+** (o repositório pode incluir uma pasta `venv/` local; prefira criar seu próprio ambiente).

```bash
cd FIAPTC3_RM367414
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
python -m pip install -U pip
python -m pip install -r requirements.txt
jupyter lab
```

Abra os notebooks a partir da **raiz** do repositório (`FIAPTC3_RM367414`), para que os caminhos `flights.csv` e `data/` funcionem como definido no código.

### Problema de certificado SSL (macOS)

Se o `pip` falhar por SSL:

```bash
python -m pip install -r requirements.txt \
  --trusted-host pypi.org \
  --trusted-host pypi.python.org \
  --trusted-host files.pythonhosted.org
```

---

## Stack técnica

- **Manipulação e visualização:** pandas, numpy, matplotlib, seaborn  
- **ML:** scikit-learn (pré-processamento, Random Forest, regressão logística, K-Means, PCA, métricas e validação cruzada)  
- **Leitura de dados:** CSV (opcionalmente via pyarrow, conforme dependências)

---

## Autoria

FIAP — Tech Challenge — **RM367414**.
