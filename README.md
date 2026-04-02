# 1. Importação das bibliotecas e carga dos dados
import pandas as pd
import seaborn as srn
import matplotlib.pyplot as plt
import os

# Carregando o dataset (ajuste o caminho se necessário)
dataset = pd.read_csv('tempo.csv', sep=';')

# --- DIAGNÓSTICO INICIAL ---
print("--- Primeiras 5 linhas ---")
print(dataset.head())
print("\n--- Informações de Colunas e Tipos ---")
print(dataset.info())
print("\n--- Contagem de Valores Nulos ---")
print(dataset.isnull().sum())

# --- ANÁLISE DE COLUNAS CATEGÓRICAS ---
# Verificando domínios (Aparência, Vento e Jogar)

cols_cat = ['Aparencia', 'Vento', 'Jogar']

for col in cols_cat:
    print(f"\n--- Agrupamento da coluna: {col} ---")
    print(dataset.groupby([col]).size())
    plt.figure(figsize=(6,4))
    srn.countplot(x=col, data=dataset, palette='viridis').set_title(f'Distribuição: {col}')
    plt.show()

# --- ANÁLISE DE COLUNAS NUMÉRICAS (OUTLIERS) ---
# Verificando Temperatura e Umidade

print("\n--- Estatísticas Descritivas (Numéricas) ---")
print(dataset.describe())

# Visualização de Outliers com Boxplot


plt.figure(figsize=(12, 5))

# Subplot Temperatura
plt.subplot(1, 2, 1)
srn.boxplot(y=dataset['Temperatura'], color='orange').set_title('Distribuição de Temperatura')

# Subplot Umidade
plt.subplot(1, 2, 2)
srn.boxplot(y=dataset['Umidade'], color='green').set_title('Distribuição de Umidade')

plt.tight_layout()
plt.show()

# --- SALVANDO O TRABALHO ---
# Salvando o DataFrame analisado (caso tenha feito alterações)
dataset.to_csv('tempo_analisado.csv', index=False, sep=';')
print("\nArquivo 'tempo_analisado.csv' salvo com sucesso!")
