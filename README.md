### Atividade 1 | Banco de Dados Não Relacionais


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
);
```

1.2 Insira pelo menos 5 registros com diferentes clientes e diferentes datas de  pedidos.

```cql
INSERT INTO pedidos (
  id_cliente,
  data,
  id_pedido,
  valor,
  status)
VALUES (1, '2024-09-20', 100, 1000, 'em trânsito'),
      (2, '2024-09-21', 200, 2000, 'em trânsito'),
      (3, '2024-09-22', 300, 3000, 'em trânsito'),
      (4, '2024-09-23', 400, 4000, 'em trânsito'),
      (5, '2024-09-24', 500, 5000, 'em trânsito'),
      (1, '2024-09-22', 100, 1000, 'finalizado'),
      (2, '2024-09-23', 200, 2000, 'finalizado'),
      (3, '2024-09-24', 300, 3000, 'finalizado'),
      (4, '2024-09-25', 400, 4000, 'finalizado'),
      (5, '2024-09-26', 500, 5000, 'finalizado'),
);
```

1.3 Execute consultas para:
- Buscar todos os pedidos de um cliente específico, ordenados pela data.
- Filtrar os pedidos de um cliente em um determinado intervalo de datas.

```cql
-- Buscar todos os pedidos de um cliente específico, ordenados pela data.
SELECT *
FROM pedidos
WHERE id_cliente = 1
ORDER BY (data ASC);
```

```cql
-- Filtrar os pedidos de um cliente em um determinado intervalo de datas.
SELECT *
FROM pedidos
WHERE id_cliente = 1
AND data >= '2024-09-20'
AND data <= '2024-09-22';
```

2.1 Crie uma tabela chamada produtos, que incluirá:
- id (int) como chave primária ou chave de partição.
- nome (text).
- avaliacoes (LIST<int>) para armazenar as avaliações dos produtos.

```cql
-- A coluna id é a chave primária ou partição.

CREATE TABLE produtos (
  id int,
  nome text,
  avaliacoes LIST int
PRIMARY KEY (id)
);
```

2.2 Insira pelo menos 3 produtos e adicione 3 avaliações diferentes para cada um 
usando o comando UPDATE.

```cql
-- Insira pelo menos 3 produtos
INSERT INTO pedidos (
  id,
  nome
)
VALUES
(1, "Oreo"),
(2, "Bono"),
(3, "Nesfit");
```

```cql
-- adicione 3 avaliações diferentes para cada um usando o comando UPDATE.
UPDATE produtos
SET avaliacoes = avaliacoes + [4,5,5]
WHERE id = 1;
UPDATE produtos
SET avaliacoes = avaliacoes + [1,2,2]
WHERE id = 2;
UPDATE produtos
SET avaliacoes = avaliacoes + [5,5,5]
WHERE id = 3;
```

2.3 Adicione uma nova avaliação a um dos produtos sem substituir as avaliações existentes.
```cql
UPDATE produtos
SET avaliacoes = avaliacoes + [2]
WHERE id = 1;
```
