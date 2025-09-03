


Este projeto tem como objetivo **limpar e normalizar** dados de produtos automotivos que estão em formato CSV, resolvendo problemas comuns de formatação e inconsistências encontradas em datasets reais.


### 💰 Preços em Formatos Variados
- `100` → `100.00`
- `R$100` → `100.00`
- `"R$1.250,00"` → `1250.00`
- `"100,50"` → `100.50`
- `R$ 200,00` → `200.00`

### 📦 Valores de Estoque Inválidos
- `-1` → `0`
- `None` → `0`
- `n/a` → `0`
- Campos vazios → `0`

### 🏷️ Nomes de Produtos com Problemas / strip, (stripados)
- `" Bieleta  "` → `"Bieleta"`
- Remoção de espaços extras

## 📋 Estrutura do Projeto

```
Teste_Fuçar/
├── 📄 Teste.py                 # Script principal de limpeza
├── 📊 produtos_limpos.csv      # Arquivo de saída com dados limpos
├── 📖 README.md               # Este arquivo
└── 🔧 .venv/                  # Ambiente virtual Python
    └── Scripts/
        └── python.exe         # Interpretador Python isolado
└── ⚙️ .vscode/                # Configurações do VS Code
    └── settings.json          # Configurações do Rainbow CSV
```

## 🛠️ Tecnologias Utilizadas

- **Python 3.13+**
- **Pandas** - Manipulação e análise de dados
- **io** - Manipulação de fluxos de dados



### 1. Clone ou Baixe o Projeto
```bash
# Se usando Git
git clone <url-do-repositorio>
cd Teste_Fuçar



### 2. Configure o Ambiente Virtual
```powershell
# Criar ambiente virtual (se não existir)
python -m venv .venv

# Ativar ambiente virtual
.\.venv\Scripts\Activate.ps1

# Instalar dependências
pip install pandas
```

### 3. Execute o Script
```powershell
# Com ambiente virtual ativo
python Teste.py

# Ou diretamente
.\.venv\Scripts\python.exe Teste.py
```

## 🎮 Como Usar

### Execução Básica
1. Abra o terminal no diretório do projeto
2. Execute o script: `python Teste.py`
3. Observe a saída detalhada no terminal
4. Verifique o arquivo `produtos_limpos.csv` gerado

### Personalizando os Dados
Para usar seus próprios dados, edite a variável `csv_data` no arquivo `Teste.py`:

```python
csv_data = """nome_produto,codigo,preco,estoque
Seu Produto,ABC123,R$ 150,50
Outro Produto,XYZ789,"1.500,00",25
"""
```

## 📊 Exemplo de Saída

### Dados de Entrada (Brutos)
```
nome_produto          | codigo    | preco        | estoque
 Bieleta              | K45454LA  | "100,50"     | 2
Lanterna Traseira     | K33445EU  | "R$1.250,00" | 
Radiador              | K66666LA  | R$99         | 90
```

### Dados de Saída (Limpos)
```
nome_produto          | codigo    | preco   | estoque
Bieleta              | K45454LA  | 100.50  | 2
Lanterna Traseira    | K33445EU  | 1250.00 | 0
Radiador             | K66666LA  | 99.00   | 90
```

## 🔍 Análise Detalhada do Código

### Função Principal: `normalizar_preco()`

```python
def normalizar_preco(valor) -> float:
    """
    Normaliza valores de preço em diferentes formatos brasileiros.
    
    Lógica:
    1. Remove símbolos de moeda (R$) e espaços
    2. Detecta formato brasileiro: "1.250,00"
    3. Detecta vírgula decimal: "100,50"
    4. Mantém formato americano: "100.50"
    5. Converte para float ou retorna 0.0 em caso de erro
    """
```

### Etapas de Processamento

1. **📋 Carregamento**: Lê dados CSV usando `pandas.read_csv()`
2. **💰 Preços**: Normaliza formato monetário brasileiro
3. **📦 Estoque**: Substitui valores inválidos por 0
4. **🏷️ Nomes**: Remove espaços extras
5. **💾 Salvamento**: Exporta dados limpos para CSV
6. **📊 Relatório**: Exibe estatísticas e preview


## 🐛 Solução de Problemas

### Erro: "ModuleNotFoundError: No module named 'pandas'"
```powershell
# Ative o ambiente virtual
.\.venv\Scripts\Activate.ps1

# Instale pandas
pip install pandas
```


### Caracteres especiais não aparecem
O script usa `encoding='utf-8-sig'` para resolver problemas de acentuação em programas como Excel.
