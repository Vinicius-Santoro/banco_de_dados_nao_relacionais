# Banco de Dados Não Relacionais


Repositório para armazenar a atividade 1 de bancos de dados não relacionais

1.1 Crie uma tabela chamada pedidos para armazenar informações de pedidos de uma loja. A tabela deve incluir:
- id_cliente (int) como chave de partição.
- data (timestamp) como chave de clustering para ordenar os pedidos pela data.
- id_pedido (int) como chave de clustering secundária.
- Outras colunas: valor (float), status (text).

```cql
-- A coluna id_cliente é a chave de partição, já id_pedido é a chave de clustering.

CREATE TABLE pedidos (
  id_cliente int,
  data timestamp,
  id_pedido int,
  valor float,
  status text,
PRIMARY KEY ((id_cliente), id_pedido)
)
```

1.2 Insira pelo menos 5 registros com diferentes clientes e diferentes datas de  pedidos.

```cql
-- A coluna id_cliente é a chave de partição, já id_pedido é a chave de clustering.

INSERT INTO pedidos (
  id_cliente,
  data,
  id_pedido,
  valor,
  status)
VALUES (1, '2024-09-20', 100, 1000, 'finalizado',
        2, '2024-09-21', 200, 2000, 'em trânsito',
        3, '2024-09-22', 300, 3000, 'em trânsito',
        4, '2024-09-23', 400, 4000, 'preparando',
        5, '2024-09-24', 500, 5000, 'em trânsito',
)

```
