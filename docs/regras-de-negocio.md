# Regras de Negócio do StockFlow

## RN01 — Conferência da quantidade

A quantidade física recebida deve ser conferida com a quantidade informada na nota fiscal.

## RN02 — Quantidade efetivamente recebida

A quantidade adicionada ao estoque deve corresponder à quantidade física efetivamente recebida.

## RN03 — Divergência de quantidade

Quando houver diferença entre a quantidade informada na nota fiscal e a quantidade recebida, a entrada da mercadoria não deve ser bloqueada.

A divergência deverá ser registrada no sistema com uma observação.

## RN04 — Tratamento da divergência

No MVP, o StockFlow deverá apenas registrar a divergência.

A entrega posterior do produto faltante ou o recebimento de crédito do fornecedor não serão controlados pelo sistema inicialmente.

## RN05 — Valor dos produtos

Os produtos possuem preço tabelado. Portanto, o processo de recebimento não deverá permitir negociação de preço.

## RN06 — Conferência do pedido

Durante o recebimento, o usuário deve confirmar se a mercadoria recebida corresponde ao pedido realizado anteriormente ao fornecedor.

## RN07 — Produto não cadastrado

Quando um produto da nota fiscal não estiver cadastrado, o sistema deverá informar o usuário e oferecer a opção de realizar o cadastro.

## RN08 — Prazo de pagamento

Os prazos de pagamento considerados inicialmente pelo sistema serão:

- 7 dias
- 14 dias
- 21 dias

## RN09 — Data de vencimento

A data de vencimento da conta a pagar será calculada a partir da data de emissão/saída da nota fiscal e do prazo de pagamento definido.

## RN10 — Contas a pagar

Ao efetivar a entrada da nota fiscal, o sistema deverá registrar a respectiva conta a pagar utilizando o valor total da nota fiscal.

## RN11 — Estoque

A entrada de uma nota fiscal deverá atualizar a quantidade em estoque dos produtos recebidos.

## RN12 — Integração entre processos

A confirmação da entrada de uma nota fiscal deverá resultar na atualização do estoque e no registro da conta a pagar.

## RN13 — Histórico

Uma nota fiscal efetivada deverá permanecer registrada no sistema para consulta posterior.