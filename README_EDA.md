### EDA do `flights.csv`

Arquivos gerados:
- `eda_flights.ipynb`: notebook com estatísticas, gráficos e tratamento de ausentes
- `requirements.txt`: dependências

### Como executar

```bash
cd /Users/kauan.silva/Desktop/TC3
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -U pip
python -m pip install -r requirements.txt
jupyter lab
```

Se o `pip` falhar com erro de certificado SSL no macOS, use:

```bash
python -m pip install -r requirements.txt \
  --trusted-host pypi.org \
  --trusted-host pypi.python.org \
  --trusted-host files.pythonhosted.org
```

