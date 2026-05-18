# Bug Report

## Título

Divergência entre total exibido no checkout e total persistido no pedido após aplicação de cupom

## Resumo

Alguns usuários relatam que conseguem aplicar um cupom com sucesso no checkout, visualizam o desconto corretamente na interface, mas ao finalizar a compra o valor do pedido gerado não respeita o desconto aplicado.

## Impacto

- risco financeiro
- perda de confiança do usuário
- aumento de chamados de suporte
- possível falha de integridade entre serviços

## Logs Disponíveis

```txt
INFO ApplyCouponService - coupon=BEMVINDO10 user=4821 cart=9912
INFO CartTotals - subtotal=250 shipping=20 discount=25 total=245
INFO CheckoutService - order=55310 subtotal=250 shipping=20 total=270
WARN DivergentTotals - cart=9912 order=55310
```

## Perguntas Para Guiar Sua Análise

- O que os logs indicam sobre o ponto de divergência?
- Em que camada essa inconsistência pode estar ocorrendo?
- Quais dados você pediria ao time para aprofundar a investigação?
- Que testes de regressão você criaria após a correção?
