# Modelo do Banco de Dados

## 1. Objetivo

O banco de dados do StockFlow será responsável por armazenar e organizar as informações relacionadas aos produtos, fornecedores, notas fiscais, itens das notas e contas a pagar.

A modelagem foi pensada inicialmente para atender ao MVP do sistema, permitindo que a aplicação controle o processo de recebimento de mercadorias, entrada no estoque e registro das contas a pagar.

## 2. Entidade Produto

A entidade Produto armazenará as informações dos produtos comercializados pelo estabelecimento.

### Principais atributos

- id
- código
- código de barras
- descrição
- marca
- preço de custo
- preço de venda
- estoque mínimo
- quantidade em estoque
- situação

## 3. Entidade Fornecedor

A entidade Fornecedor armazenará os dados dos fornecedores que realizam a venda de mercadorias para o estabelecimento.

### Principais atributos

- id
- razão social
- nome fantasia
- CNPJ

## 4. Entidade Nota Fiscal

A entidade Nota Fiscal armazenará as informações principais das notas fiscais recebidas dos fornecedores.

Ela será utilizada como base para o processo de conferência, entrada das mercadorias e geração da conta a pagar.

### Principais atributos

- id
- número
- série
- data de emissão
- valor total
- condição de pagamento
- status
- fornecedor_id

## 5. Entidade Item da Nota Fiscal

A entidade Item da Nota Fiscal representará cada produto que faz parte de uma nota fiscal.

Uma nota fiscal pode possuir vários itens, e cada item estará relacionado a um produto cadastrado no sistema.

### Principais atributos

- id
- nota_fiscal_id
- produto_id
- quantidade
- valor unitário
- valor total

## 6. Entidade Conta a Pagar

A entidade Conta a Pagar armazenará as parcelas financeiras relacionadas às notas fiscais recebidas.

Uma nota fiscal poderá gerar uma ou mais parcelas, de acordo com a condição de pagamento definida.

Cada parcela terá seu próprio valor, data de vencimento e status de pagamento.

### Principais atributos

- id
- nota_fiscal_id
- número da parcela
- valor da parcela
- data de vencimento
- status

## 7. Relacionamentos entre as entidades

### 7.1 Fornecedor e Nota Fiscal

Um fornecedor pode emitir várias notas fiscais.

Cada nota fiscal pertence a apenas um fornecedor.

*Relacionamento:*

Fornecedor 1:N Nota Fiscal

A chave estrangeira fornecedor_id ficará na entidade Nota Fiscal, identificando o fornecedor responsável pela nota.

### 7.2 Nota Fiscal e Item da Nota

Uma nota fiscal pode possuir vários itens.

Cada item da nota fiscal pertence a uma única nota fiscal.

*Relacionamento:*

Nota Fiscal 1:N Item da Nota

A chave estrangeira nota_fiscal_id ficará na entidade Item da Nota, identificando a qual nota fiscal o item pertence.

### 7.3 Item da Nota e Produto

Um produto pode aparecer em vários itens de diferentes notas fiscais.

Cada item da nota fiscal corresponde a apenas um produto.

*Relacionamento:*

Produto 1:N Item da Nota

A chave estrangeira produto_id ficará na entidade Item da Nota, identificando qual produto está sendo registrado naquele item.

### 7.4 Nota Fiscal e Conta a Pagar

Uma nota fiscal pode gerar uma ou mais parcelas a pagar, de acordo com a condição de pagamento.

Cada parcela da conta a pagar pertence a uma única nota fiscal.

*Relacionamento:*

Nota Fiscal 1:N Conta a Pagar

A chave estrangeira nota_fiscal_id ficará na entidade Conta a Pagar, identificando a qual nota fiscal a parcela pertence.

### 7.5 Item da Nota e Conferência

Um item da nota fiscal pode possuir várias conferências.

Cada conferência pertence a um único item da nota fiscal.

*Relacionamento:*

Item da Nota 1:N Conferência

A chave estrangeira item_nota_id ficará na entidade Conferência, identificando a qual item da nota fiscal a conferência pertence.

## 8. Resumo do Modelo

O banco de dados do StockFlow será composto pelas seguintes entidades:

- Produto
- Fornecedor
- Nota Fiscal
- Item da Nota
- Conferência
- Conta a Pagar

### Relacionamentos

- Um fornecedor pode possuir várias notas fiscais.
- Uma nota fiscal pertence a um único fornecedor.
- Uma nota fiscal pode possuir vários itens.
- Cada item pertence a uma única nota fiscal.
- Um produto pode aparecer em vários itens de notas fiscais.
- Cada item corresponde a um único produto.
- Uma nota fiscal pode gerar uma ou mais parcelas de contas a pagar.
- Cada parcela pertence a uma única nota fiscal.
- Um item da nota pode possuir várias conferências.
- Cada conferência pertence a um único item da nota.

### Estrutura conceitual

Fornecedor 1:N Nota Fiscal

Nota Fiscal 1:N Item da Nota

Produto 1:N Item da Nota

Nota Fiscal 1:N Conta a Pagar

Item da Nota 1:N Conferência


## 9. Diagrama Entidade-Relacionamento

```mermaid
erDiagram

    FORNECEDOR ||--o{ NOTA_FISCAL : possui
    NOTA_FISCAL ||--|{ ITEM_NOTA : possui
    PRODUTO ||--o{ ITEM_NOTA : aparece_em
    NOTA_FISCAL ||--|{ CONTA_A_PAGAR : gera
    ITEM_NOTA ||--o{ CONFERENCIA : possui

    FORNECEDOR {
        bigint id PK
        string razao_social
        string nome_fantasia
        string cnpj
    }

    PRODUTO {
        bigint id PK
        string codigo
        string codigo_barras
        string descricao
        string marca
        decimal preco_custo
        decimal preco_venda
        decimal estoque_minimo
        decimal quantidade_estoque
        boolean ativo
    }

    NOTA_FISCAL {
        bigint id PK
        string numero
        string serie
        date data_emissao
        decimal valor_total
        string condicao_pagamento
        string status
        bigint fornecedor_id FK
    }

    ITEM_NOTA {
        bigint id PK
        bigint nota_fiscal_id FK
        bigint produto_id FK
        decimal quantidade
        decimal valor_unitario
        decimal valor_total
    }

    CONFERENCIA {
        bigint id PK
        bigint item_nota_id FK
        decimal quantidade_recebida
        string status
        string observacao
        datetime data_conferencia
    }

    CONTA_A_PAGAR {
        bigint id PK
        bigint nota_fiscal_id FK
        integer numero_parcela
        decimal valor_parcela
        date data_vencimento
        string status
    }