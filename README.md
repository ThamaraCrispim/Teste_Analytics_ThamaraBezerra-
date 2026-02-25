#  Teste de Analytics – Estagiário de Analytics

Este repositório contém a solução para o teste de estágio em Analytics.  
O projeto consiste na simulação, limpeza, análise exploratória e consultas SQL de um dataset de vendas de uma loja de materiais de construção, com o objetivo de extrair insights de negócio acionáveis.

---

##  Estrutura do Repositório

- `Teste_Analytics_ThamaraBezerra.ipynb` – Notebook principal com simulação, limpeza, análise, gráficos e integração com SQL.
- `consultas_sql_sql.ipynb` – Notebook com as consultas SQL executadas.
- `dados_brutos.csv` – Dataset antes da limpeza (com valores nulos).
- `dados_limpos.csv` – Dataset tratado (sem nulos e com coluna `Total_Vendas`).
- `relatorio_insights.md` – Relatório resumido com insights e recomendações.
- `requisitos.txt` – Bibliotecas necessárias para execução.

---


## Sobre os Dados

###  Simulação

- 200 registros de vendas
- Período: 01/01/2023 a 31/12/2023
- Variáveis:
  -ID
  - Data
  - Produto
  - Categoria
  - Quantidade
  - Preço

Foram inseridos aproximadamente 5% de valores nulos em `Quantidade` e `Preço` para simular imperfeições reais.

---

###  Limpeza

- Nulos em `Quantidade` → preenchidos com mediana da categoria.
- Nulos em `Preço` → preenchidos com média do produto.
- Conversão de tipos realizada.
- Criação da coluna `Total_Vendas = Quantidade × Preço`.
- Não foram encontradas duplicatas.

---

## Análises Realizadas

###  Python

- Estatísticas descritivas
- Faturamento por categoria
- Top 5 produtos por faturamento
- Evolução mensal das vendas
- Boxplot mensal
- Gráfico de barras por produto

Principais achados:

- Categoria Estrutural lidera o faturamento.
- Tijolo Cerâmico representa ~70% da receita total.
- Picos em fevereiro, maio e dezembro.
- Julho é o mês mais fraco.
- Ferramentas têm maior volume de transações, mas menor ticket médio.

---

### SQL

Banco SQLite em memória criado a partir do DataFrame tratado.

#### Consulta 1 – Faturamento total por produto

```sql
SELECT Produto, Categoria, SUM(Quantidade * Preço) AS Total_Vendas
FROM vendas
GROUP BY Produto, Categoria
ORDER BY Total_Vendas DESC;
```

Resultado: Tijolo Cerâmico lidera com R$ 369,7 mil.

---

#### Consulta 2 – Produtos com menor faturamento em junho/2023

```sql
SELECT Produto, SUM(Quantidade * Preço) AS Total_Vendas_Junho
FROM vendas
WHERE strftime('%Y-%m', Data) = '2023-06'
GROUP BY Produto
ORDER BY Total_Vendas_Junho ASC
LIMIT 5;
```

Observação: A consulta original mencionava junho/2024. Como os dados simulados são de 2023, o filtro foi ajustado para manter coerência analítica.

---

## Principais Insights

1. Alta concentração de receita no Tijolo Cerâmico (~70%).
2. Sazonalidade clara com picos em fevereiro, maio e dezembro.
3. Produtos de baixo desempenho recorrente (Martelo, Trena, Cimento, Piso, Areia).
4. Categoria Ferramentas possui alto volume, mas baixo ticket médio.

---

## Dependências

- pandas  
- numpy  
- matplotlib  
- seaborn  
- sqlite3  

Versões detalhadas em `requisitos.txt`.

---

##  Observações Finais

- A simulação buscou variação realista de preço e quantidade.
- O tratamento de nulos preservou registros.
- A adaptação da consulta para 2023 foi devidamente justificada.
- O projeto priorizou organização, clareza e reprodutibilidade.

---

**Autora:** Thamara Bezerra  
**Data:** Fevereiro/2025  
**Contato:** Thamaragabriela26@gmail.com
