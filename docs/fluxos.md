
## 1. Fluxo principal — Recebimento de mercadoria

O processo principal do StockFlow começa quando uma mercadoria solicitada ao fornecedor é recebida.

Pedido realizado ao fornecedor
            ↓
    Mercadoria recebida
            ↓
       Conferência
            ↓
 ┌───────────────────────┐
 │ Conferir quantidade   │
 │ física x nota fiscal  │
 │ Conferir pedido       │
 │ Conferir prazo        │
 └───────────────────────┘
            ↓
    Houve divergência?
       ↙️           ↘️
     NÃO           SIM
      ↓             ↓
      │       Registrar divergência
      │       e observação
      │             ↓
      └───────┬─────┘
              ↓
      Confirmar entrada
              ↓
      Atualizar estoque
              ↓
     Registrar conta
        a pagar

## 2. Fluxo de conferência da quantidade

Durante a conferência, o usuário deverá comparar a quantidade informada na nota fiscal com a quantidade física recebida.

Quantidade da NF
       +
Quantidade recebida
       ↓
    Comparação
       ↓
São iguais?
   ↙️       ↘️
 SIM       NÃO
  ↓          ↓
Continuar   Registrar
conferência divergência
             ↓
        Continuar entrada

Quando houver divergência, o sistema deverá permitir registrar uma observação.

A entrada não deverá ser bloqueada.

⸻

##3. Fluxo de produto não cadastrado

Durante o lançamento dos itens da nota, o sistema deverá verificar se o produto está cadastrado.

Produto informado
       ↓
Produto cadastrado?
     ↙️       ↘️
   SIM       NÃO
    ↓          ↓
Continuar   Informar usuário
             ↓
       Deseja cadastrar?
          ↙️       ↘️
        SIM       NÃO
         ↓         ↓
      Cadastrar   Interromper/
      produto     tratar item
         ↓
      Continuar

##4. Fluxo de contas a pagar

Após a confirmação da entrada da nota fiscal, o sistema deverá registrar a conta a pagar.

Nota fiscal confirmada
          ↓
Valor total da nota
          +
Prazo de pagamento
          ↓
   Calcular vencimento
          ↓
Registrar conta a pagar

Os prazos inicialmente considerados são:

* 7 dias
* 14 dias
* 21 dias

A data de vencimento será calculada a partir da data de emissão/saída da nota fiscal.

⸻

##5. Fluxo de atualização do estoque

Após a confirmação da entrada da nota, o estoque deverá ser atualizado utilizando a quantidade efetivamente recebida.

Entrada da nota confirmada
           ↓
Identificar produto
           ↓
Quantidade efetivamente recebida
           ↓
Adicionar ao estoque
           ↓
Novo saldo do estoque

## 6.Fluxo completo do MVP

PEDIDO AO FORNECEDOR
          ↓
RECEBIMENTO
          ↓
CONFERÊNCIA
          ↓
 ┌─────────────────────────┐
 │ Quantidade              │
 │ Pedido                  │
 │ Prazo de pagamento      │
 └─────────────────────────┘
          ↓
   Produto cadastrado?
      ↙️           ↘️
    SIM           NÃO
     ↓             ↓
     │       Cadastrar produto
     │             ↓
     └───────┬─────┘
             ↓
     Houve divergência?
        ↙️           ↘️
      NÃO           SIM
       ↓             ↓
       │       Registrar observação
       │             ↓
       └───────┬─────┘
               ↓
       CONFIRMAR ENTRADA
               ↓
       ┌───────┴────────┐
       ↓                ↓
   ATUALIZAR         REGISTRAR
    ESTOQUE        CONTAS A PAGAR

##PEDIDO AO FORNECEDOR
          ↓
RECEBIMENTO
          ↓
CONFERÊNCIA
          ↓
 ┌─────────────────────────┐
 │ Quantidade              │
 │ Pedido                  │
 │ Prazo de pagamento      │
 └─────────────────────────┘
          ↓
   Produto cadastrado?
      ↙️           ↘️
    SIM           NÃO
     ↓             ↓
     │       Cadastrar produto
     │             ↓
     └───────┬─────┘
             ↓
     Houve divergência?
        ↙️           ↘️
      NÃO           SIM
       ↓             ↓
       │       Registrar observação
       │             ↓
       └───────┬─────┘
               ↓
       CONFIRMAR ENTRADA
               ↓
       ┌───────┴────────┐
       ↓                ↓
   ATUALIZAR         REGISTRAR
    ESTOQUE        CONTAS A PAGAR

## 7. Situação futura — Importação de XML

A importação do XML da NF-e será implementada em uma versão futura.

O fluxo planejado será:

Upload do XML
      ↓
Leitura dos dados da NF-e
      ↓
Identificação dos produtos
      ↓
Conferência
      ↓
Entrada no estoque
      ↓
Contas a pagar



