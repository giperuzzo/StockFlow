# Requisitos do StockFlow

## 1. Objetivo

O StockFlow tem como objetivo facilitar o controle de entradas de mercadorias, estoque e contas a pagar de pequenos comércios, reduzindo a necessidade de controles manuais.

O sistema será desenvolvido inicialmente com foco no processo de recebimento e entrada de mercadorias a partir das notas fiscais recebidas dos fornecedores.

---

## 2. Escopo do MVP

A primeira versão do StockFlow deverá permitir:

- Cadastro de produtos
- Cadastro de fornecedores
- Cadastro de notas fiscais
- Cadastro dos itens da nota fiscal
- Conferência da nota fiscal
- Registro de divergências de quantidade
- Entrada dos produtos no estoque
- Controle de contas a pagar
- Consulta do histórico de notas fiscais

---

## 3. Requisitos Funcionais

### RF01 — Cadastro de produtos

O sistema deve permitir cadastrar produtos informando seus principais dados.

Os produtos deverão possuir, inicialmente, informações como:

- Código
- Código de barras
- Descrição
- Marca
- Preço de custo
- Preço de venda
- Estoque mínimo
- Quantidade em estoque
- Situação do cadastro

---

### RF02 — Cadastro de fornecedores

O sistema deve permitir cadastrar fornecedores.

O cadastro deverá conter, inicialmente:

- Razão social
- Nome fantasia
- CNPJ

---

### RF03 — Cadastro de nota fiscal

O sistema deve permitir registrar uma nota fiscal informando seus principais dados.

A nota fiscal deverá possuir, inicialmente:

- Número
- Série
- Data de emissão
- Valor total
- Condição de pagamento
- Fornecedor

---

### RF04 — Cadastro dos itens da nota fiscal

O sistema deve permitir adicionar os produtos presentes na nota fiscal.

Cada item deverá possuir, inicialmente:

- Produto
- Quantidade informada na nota
- Valor unitário
- Valor total

---

### RF05 — Conferência da nota fiscal

O sistema deve permitir conferir a nota fiscal antes de efetivar a entrada dos produtos.

Durante a conferência, o usuário deverá verificar:

- Quantidade informada na nota fiscal;
- Quantidade física recebida;
- Prazo de pagamento;
- Se a mercadoria recebida corresponde ao pedido realizado.

Os produtos possuem preço tabelado, portanto não haverá negociação de preço durante o recebimento.

---

### RF06 — Entrada no estoque

Ao confirmar a entrada da nota, o sistema deve atualizar o estoque considerando a quantidade efetivamente recebida.

A quantidade adicionada ao estoque deverá corresponder à quantidade física recebida.

---

### RF07 — Registro de divergência

Quando houver diferença entre a quantidade informada na nota fiscal e a quantidade física recebida, o sistema deve permitir registrar a divergência.

O usuário deverá poder informar uma observação sobre a divergência.

A existência de uma divergência não deverá impedir a entrada da mercadoria no estoque.

---

### RF08 — Produto não cadastrado

Quando um produto informado na nota fiscal não estiver cadastrado, o sistema deve informar:

> "Produto X não está cadastrado. Deseja cadastrar?"

O usuário poderá optar por cadastrar o produto antes de continuar o processo de entrada da nota.

---

### RF09 — Contas a pagar

Ao efetivar uma nota fiscal, o sistema deve registrar a conta a pagar utilizando o valor da nota fiscal e o prazo de pagamento informado.

Os prazos inicialmente considerados são:

- 7 dias
- 14 dias
- 21 dias

O sistema deverá calcular a data de vencimento a partir da data utilizada para o pagamento e do prazo selecionado.

---

### RF10 — Histórico de notas fiscais

O sistema deve permitir consultar as notas fiscais já cadastradas.

A consulta deverá permitir visualizar, inicialmente:

- Número da nota
- Fornecedor
- Data de emissão
- Valor total
- Condição de pagamento
- Situação da nota

---

## 4. Requisitos Não Funcionais

### RNF01 — Interface

O sistema deve possuir uma interface simples, organizada e fácil de utilizar.

### RNF02 — Persistência dos dados

Os dados do sistema devem ser armazenados de forma persistente em um banco de dados PostgreSQL.

### RNF03 — API

O backend deverá disponibilizar uma API REST para comunicação com o frontend.

### RNF04 — Frontend

O frontend será desenvolvido utilizando Angular e TypeScript.

### RNF05 — Backend

O backend será desenvolvido utilizando Java e Spring Boot.

### RNF06 — Controle de versão

O código-fonte do projeto deverá ser versionado utilizando Git e disponibilizado no GitHub.

---

## 5. Fluxo principal do MVP

O fluxo principal do StockFlow será:

*Recebimento da mercadoria → Conferência da nota → Registro de divergência, se houver → Entrada no estoque → Registro da conta a pagar*

Durante a conferência, o sistema também deverá permitir verificar se a mercadoria recebida corresponde ao pedido realizado.

---

## 6. Funcionalidades futuras

As seguintes funcionalidades não fazem parte do MVP inicial e poderão ser desenvolvidas em versões futuras:

- Importação de XML da NF-e
- Integração com pedidos realizados no e-commerce do fornecedor
- Controle de vendas
- Baixa automática do estoque nas vendas
- Alertas de estoque mínimo
- Relatórios
- Controle de créditos de fornecedores
- Acompanhamento de divergências
- Autenticação de usuários
- Controle de permissões