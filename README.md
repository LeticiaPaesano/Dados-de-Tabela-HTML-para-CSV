# Extração de Dados de Tabela HTML para CSV

## Objetivo

Documentar o processo de extração de dados tabulares de uma página HTML para um arquivo CSV, com foco em aprendizado prático e aplicação direta da biblioteca pandas para análise de dados.

## Contexto

Foi utilizada a página da Wikipédia que lista países por população:  
https://pt.wikipedia.org/wiki/Lista_de_pa%C3%ADses_por_popula%C3%A7%C3%A3o

Para identificar as tabelas HTML disponíveis, utilizei a ferramenta de inspeção do navegador (DevTools), aplicando a busca pelo elemento `<table>`. Dessa forma, localizei todas as tabelas contidas na página para seleção posterior no código.

![Sem título](https://github.com/user-attachments/assets/9d2ea918-40bd-4185-828b-37d4821b8e61)

## Procedimento

1. Realizei a leitura das tabelas diretamente do HTML da URL usando o método `pd.read_html()`, que retorna uma lista com todos os dataframes extraídos das tabelas presentes na página.

2. Seleciono o dataframe correspondente à primeira tabela (`dados[0]`), que contém a informação relevante.

3. Para simplificar a análise e reduzir o volume de dados, extraí apenas as colunas essenciais:  
   - `País (ou território dependente)`  
   - `Estimativa da ONU`

4. Finalmente, exporto o dataframe resultante para um arquivo CSV local, sem índice, para facilitar uso posterior.

## Código

```python
import pandas as pd

url = 'https://pt.wikipedia.org/wiki/Lista_de_pa%C3%ADses_por_popula%C3%A7%C3%A3o'

# Extrai todas as tabelas da página HTML
dados = pd.read_html(url)

# Seleciona a tabela principal de países por população
df_populacao = dados[0]

# Filtra apenas as colunas relevantes
df_reduzido = df_populacao[['País (ou território dependente)', 'Estimativa da ONU']]

# Exporta para CSV local sem índice
df_reduzido.to_csv('populacao_paises.csv', index=False)
