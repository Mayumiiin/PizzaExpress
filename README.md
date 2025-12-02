# Projeto de Banco de Dados: Gerenciamento de Pedidos de Pizzaria

## 🍕 Minimundo: Pizzaria "PizzaExpress"

Este projeto de banco de dados foi desenvolvido como parte de um exercício prático de modelagem de dados, focado no minimundo de um sistema interno de gerenciamento de pedidos para uma pizzaria, o "PizzaExpress".

O objetivo principal é otimizar o processo de recebimento, preparo e entrega de pedidos, mantendo um registro estruturado de clientes, produtos, ingredientes e entregadores.

## 📐 Modelo de Dados (DER e Projeto Lógico)

O modelo de dados foi construído seguindo as melhores práticas de normalização (até a 3ª Forma Normal - 3FN) para garantir a integridade e a eliminação de redundâncias.

### Entidades Principais

| Entidade | Descrição |
| :--- | :--- |
| `CLIENTE` | Informações dos clientes que realizam os pedidos. |
| `ENTREGADOR` | Informações dos funcionários responsáveis pela entrega. |
| `PRODUTO` | Itens do cardápio (pizzas, bebidas, etc.). |
| `INGREDIENTE` | Componentes utilizados na preparação dos produtos. |
| `PRODUTO_INGREDIENTE` | Tabela associativa para o relacionamento N:N entre PRODUTO e INGREDIENTE. |
| `PEDIDO` | Registro da transação de compra (não incluída nos scripts de criação, mas essencial para o modelo lógico). |
| `ITEM_PEDIDO` | Detalha os produtos que compõem um pedido (não incluída nos scripts de criação, mas essencial para o modelo lógico). |

## 💻 Scripts SQL

O arquivo `pasted_content.txt` contém uma série de comandos SQL para a criação da estrutura do banco de dados, inserção de dados de exemplo e operações básicas de manipulação (SELECT, UPDATE, DELETE).

### Pré-requisitos

Os scripts foram escritos utilizando a sintaxe do **PostgreSQL**. Certifique-se de ter um ambiente PostgreSQL configurado para executar os comandos.

### Estrutura do Script

O script está dividido nas seguintes seções:

1.  **Criação de Tabelas (`CREATE TABLE`):** Define a estrutura das tabelas `CLIENTE`, `ENTREGADOR`, `PRODUTO`, `INGREDIENTE` e `PRODUTO_INGREDIENTE`, incluindo chaves primárias (`PRIMARY KEY`), restrições de não-nulo (`NOT NULL`) e unicidade (`UNIQUE`).
2.  **Alteração de Tabela (`ALTER TABLE`):** Adiciona a coluna `DESCRICAO` à tabela `PRODUTO`.
3.  **Comandos INSERT:** Insere dados de exemplo nas tabelas criadas (`CLIENTE`, `ENTREGADOR`, `PRODUTO`, `INGREDIENTE`, `PRODUTO_INGREDIENTE`).
4.  **Comandos SELECT:** Exemplos de consultas para recuperar dados, incluindo uma consulta `JOIN` para listar os ingredientes de um produto.
5.  **Comandos UPDATE:** Exemplos de atualização de dados nas tabelas.
6.  **Comandos DELETE:** Exemplos de exclusão de registros.

### Instruções de Uso

Para executar os scripts e interagir com o banco de dados:

1.  **Conecte-se ao seu SGBD PostgreSQL.**
2.  **Crie um novo banco de dados** (ex: `pizzaria_db`).
3.  **Execute o script em ordem:**
    *   Copie e cole o conteúdo do arquivo `pasted_content.txt` no seu cliente SQL (pgAdmin, psql, DBeaver, etc.).
    *   Execute os comandos sequencialmente, começando pelas instruções `CREATE TABLE`.

#### Exemplo de Consulta (Listar Ingredientes por Produto)

A consulta a seguir demonstra como o modelo lógico permite recuperar informações complexas, unindo as tabelas `PRODUTO`, `PRODUTO_INGREDIENTE` e `INGREDIENTE`:

```sql
SELECT
    PRODUTO.nome AS Nome_Produto,
    INGREDIENTE.nome AS Nome_Ingrediente
FROM
    PRODUTO
JOIN
    PRODUTO_INGREDIENTE ON PRODUTO.id_produto = PRODUTO_INGREDIENTE.id_produto
JOIN
    INGREDIENTE ON PRODUTO_INGREDIENTE.id_ingrediente = INGREDIENTE.id_ingrediente
WHERE
    PRODUTO.tipo = 'Pizza';
