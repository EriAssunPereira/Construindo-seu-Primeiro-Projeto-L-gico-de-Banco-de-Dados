# Construindo-seu-Primeiro-Projeto-L-gico-de-Banco-de-Dados
## Modelagem de Banco de Dados para E-Commerce

### Conceitos Fundamentais

Na modelagem de dados, existem três tipos principais:

1. **Modelagem Conceitual**: Nesta etapa, sintetizamos a estrutura do banco de dados em um nível abstrato, considerando apenas premissas básicas do negócio. É a primeira fase, onde mapeamos a estrutura macro do banco de dados com base nas especificações do plano de negócios. Por exemplo:

    ```
    Tabela Clientes (ID Cliente, Nome, CPF, RG, Email, etc)
    ```

2. **Modelagem Lógica**: Transformamos o modelo conceitual em um modelo de dados de implementação, como o modelo relacional. Aqui, definimos as tabelas, chaves primárias, chaves estrangeiras e outras restrições. É a etapa intermediária entre o conceitual e o físico.

3. **Modelagem Física**: Nesta fase, detalhamos a implementação física do banco de dados, incluindo índices, partições, tipos de dados específicos do SGBD, etc.

### Esquema Lógico para E-Commerce

Vou criar um esquema lógico para o cenário de e-commerce, considerando os refinamentos propostos:

1. **Cliente PJ e PF**:
   - Uma conta pode ser Pessoa Jurídica (PJ) ou Pessoa Física (PF).
   - Cada cliente terá informações específicas, como CNPJ (para PJ) ou CPF (para PF).

2. **Pagamento**:
   - Um cliente pode ter cadastrado mais de uma forma de pagamento (cartão de crédito, boleto, etc.).

3. **Entrega**:
   - Cada entrega possui um status (pendente, em trânsito, entregue, etc.).
   - Além disso, cada entrega tem um código de rastreio para acompanhamento.

### Exemplos de Perguntas para Embasar as Queries SQL

Aqui estão algumas perguntas que podemos responder com consultas SQL:

1. "Quais clientes têm mais de uma forma de pagamento cadastrada?"
2. "Qual é o status atual de todas as entregas?"
3. "Quais produtos foram entregues no último mês?"
Claro! Vamos abordar cada uma das suas perguntas:

1. **Quantos pedidos foram feitos por cada cliente?**
   - Para obter o número de pedidos por cliente, podemos usar uma consulta SQL que agrupe os pedidos pelo ID do cliente e conte a quantidade de pedidos. Aqui está um exemplo de consulta:
     ```sql
     SELECT cliente_id, COUNT(*) AS total_pedidos
     FROM pedidos
     GROUP BY cliente_id;
     ```
   - Essa consulta retornará o ID do cliente e o total de pedidos feitos por cada um.

2. **Algum vendedor também é fornecedor?**
   - Sim, é possível que um vendedor também atue como fornecedor. Por exemplo, um fabricante de roupas pode vender seus produtos diretamente aos clientes (como vendedor) e também fornecer roupas para outras lojas (como fornecedor).

3. **Relação de produtos, fornecedores e estoques:**
   - A relação entre produtos, fornecedores e estoques pode ser modelada em um banco de dados. Cada produto pode estar associado a um fornecedor e ter informações sobre o estoque disponível. Aqui está um exemplo de como essa relação pode ser representada:
     - Tabela `produtos`:
       - Colunas: `produto_id`, `nome`, `preco`, etc.
     - Tabela `fornecedores`:
       - Colunas: `fornecedor_id`, `nome`, `endereco`, etc.
     - Tabela `estoque`:
       - Colunas: `produto_id`, `fornecedor_id`, `quantidade_disponivel`, etc.

4. **Relação de nomes dos fornecedores e nomes dos produtos:**
   - Para obter uma lista de nomes de fornecedores e seus produtos associados, podemos usar uma consulta SQL com um `JOIN` entre as tabelas `produtos` e `fornecedores`. Aqui está um exemplo:
     ```sql
     SELECT f.nome AS nome_fornecedor, p.nome AS nome_produto
     FROM fornecedores f
     JOIN produtos p ON f.fornecedor_id = p.fornecedor_id;
     ```
   - Essa consulta retornará os nomes dos fornecedores e os nomes dos produtos que eles fornecem.
