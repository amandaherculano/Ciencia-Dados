# Ciência de Dados - Setup & Guia do Projeto

Repositório da disciplina de **Ciência de Dados** do Instituto Mauá de Tecnologia (Prof. Evandro Catelani Ferraz). Este repositório contém a estrutura recomendada de projetos, instruções completas para configuração de ambientes em **Python** e **R**, e comandos necessários para reproducibilidade em diferentes máquinas.

---

## 📁 Estrutura do Projeto

A organização de diretórios do repositório segue o padrão abaixo, garantindo a separação entre dados brutos, dados processados, códigos e saídas:

```text
ciencia-dados/
├── data/
│   ├── raw/          # Dados originais (nunca modificados)
│   └── processed/    # Dados após limpeza e tratamento
├── notebooks/        # Notebooks Jupyter (.ipynb)
├── scripts/          # Scripts Python (.py) e R (.R)
├── output/
│   ├── figures/      # Gráficos e visualizações geradas
│   └── reports/      # Relatórios exportados
├── .gitignore        # Regras de arquivos/pastas ignorados pelo Git
├── README.md         # Documentação principal do projeto
├── requirements.txt  # Dependências do Python (pip freeze)
├── renv.lock         # Mapeamento do ambiente R (renv)
└── ciencia-dados.Rproj # Arquivo de projeto do RStudio
```

---

## 💻 Como Rodar este Projeto em Outro Computador

Para clonar e executar o projeto em uma nova máquina (laboratório ou computador pessoal), siga os passos de acordo com a linguagem/ambiente desejado.

### 🐍 1. Executando o Ambiente Python

#### **No Windows (Prompt de Comando - cmd):**
```bash
# 1. Navegue até a pasta raiz do projeto
cd ciencia-dados

# 2. Crie o ambiente virtual
python -m venv .venv

# 3. Ative o ambiente virtual
.venv\Scripts\activate.bat

# 4. Atualize o pip e instale as dependências
python -m pip install --upgrade pip
pip install -r requirements.txt
```

#### **No Windows (PowerShell):**
```powershell
# Caso a execução de scripts esteja bloqueada, execute uma única vez:
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned

# 1. Navegue até a pasta raiz do projeto
cd ciencia-dados

# 2. Crie o ambiente virtual
python -m venv .venv

# 3. Ative o ambiente virtual
.venv\Scripts\Activate.ps1

# 4. Atualize o pip e instale as dependências
python -m pip install --upgrade pip
pip install -r requirements.txt
```

#### **No macOS / Linux:**
```bash
# 1. Navegue até a pasta raiz do projeto
cd ciencia-dados

# 2. Crie o ambiente virtual
python3 -m venv .venv

# 3. Ative o ambiente virtual
source .venv/bin/activate

# 4. Atualize o pip e instale as dependências
python3 -m pip install --upgrade pip
pip install -r requirements.txt
```

> **Atenção (VS Code):** Após ativar o ambiente, abra o VS Code, selecione o interpretador Python apontando para `.venv/bin/python` (ou `.venv\Scripts\python.exe`) via `Ctrl+Shift+P` > `Python: Select Interpreter`.

---

### 📊 2. Executando o Ambiente R

1. Abra o RStudio e selecione o projeto clicando duas vezes no arquivo `ciencia-dados.Rproj` (ou via `File > Open Project`).
2. Se estiver utilizando o gerenciador de dependências `renv`, execute no Console do R para restaurar exatamente os pacotes e versões originais:

```r
# Instale o renv caso ainda não possua
install.packages("renv")

# Restaure os pacotes mapeados no renv.lock
renv::restore()
```

---

## 🛠️ Pacotes e Bibliotecas Utilizados

### **Python**
* **Análise & Manipulação:** `numpy`, `pandas`, `scipy`, `statsmodels`
* **Visualização:** `matplotlib`, `seaborn`
* **Machine Learning:** `scikit-learn`
* **Ambiente Interativo:** `jupyterlab`, `ipykernel`
* **Dataset:** `palmerpenguins`

### **R (Tidyverse & Auxiliares)**
* **Tidyverse:** `dplyr`, `ggplot2`, `tidyr`, `readr`, `purrr`, `tibble`, `stringr`, `forcats`
* **Inspecção & Utilitários:** `skimr`, `janitor`, `scales`, `here`, `palmerpenguins`, `renv`

---

## 🧪 Teste de Sanidade (Sanity Check)

Para garantir que o ambiente foi montado com sucesso, execute os testes abaixo:

### **Python**
```python
import sys
import numpy as np
import pandas as pd
import matplotlib
from palmerpenguins import load_penguins

print("Python:", sys.version.split()[0])
print("NumPy:", np.__version__)
print("Pandas:", pd.__version__)
print("Matplotlib:", matplotlib.__version__)

penguins = load_penguins()
print("Penguins Shape:", penguins.shape)
print(penguins.head())
```

### **R**
```r
library(tidyverse)
library(palmerpenguins)

print(R.version.string)
print(packageVersion("dplyr"))
print(packageVersion("ggplot2"))

print(dim(penguins))
print(head(penguins))
```

---

## 📋 Regras de Ouro & Boas Práticas

1. **Caminhos Relativos:** Sempre utilize caminhos relativos a partir da raiz do projeto (ex: `data/raw/dados.csv` ou `here("data", "raw", "dados.csv")`). Nunca use caminhos absolutos (`C:\Users\...`).
2. **Dados Preservados:** Nunca altere ou sobrescreva arquivos na pasta `data/raw/`. Dados limpos devem ser gravados em `data/processed/`.
3. **Execução Sequencial:** Em notebooks Jupyter, garanta que todas as células rodem do topo para baixo. Utilize `Kernel > Restart & Run All` antes de dar push.
4. **Git:** Mantenha o arquivo `.gitignore` atualizado para não commitar ambientes virtuais (`.venv/`), dados sensíveis ou cache.
