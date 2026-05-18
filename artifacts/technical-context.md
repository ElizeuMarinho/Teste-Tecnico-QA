# Complemento Técnico

Use este material apenas como apoio para uma resposta curta. Não é necessário criar uma aplicação ou executar os exemplos.

## Trecho de Código

Considere que este trecho simplificado faz parte do fechamento do pedido:

```php
<?php

function closeOrder(array $cart): array
{
    $subtotal = $cart['subtotal'];
    $shipping = $cart['shipping'];

    $total = $subtotal + $shipping;

    return [
        'subtotal' => $subtotal,
        'shipping' => $shipping,
        'discount' => 0,
        'total' => $total,
        'coupon_code' => $cart['coupon_code'] ?? null,
    ];
}
```

Perguntas possíveis:

- Qual risco esse código traz para a regra de cupom?
- Que teste unitário ou de integração você sugeriria?
- Que informação adicional você pediria ao dev antes de validar a correção?

## Modelo de Dados Simplificado

```sql
orders(
  id,
  user_id,
  cart_id,
  subtotal,
  shipping,
  discount,
  total,
  coupon_code,
  created_at
)

cart_totals(
  cart_id,
  subtotal,
  shipping,
  discount,
  total,
  calculated_at
)
```

Pergunta possível:

- Como você encontraria pedidos onde o total do pedido ficou diferente do último total calculado para o carrinho?

## Pipeline

Considere que o projeto usa:

- `npm test` para testes de API/automação
- `composer test` para testes `PHP`

Perguntas possíveis:

- Que etapa mínima você colocaria em `GitHub Actions` para prevenir regressão?
- Que teste deveria bloquear o merge depois da correção?
