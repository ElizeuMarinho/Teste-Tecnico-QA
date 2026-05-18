# API Spec

## `POST /login`

Autentica o usuário e retorna um token.

### Request

```json
{
  "email": "qa.candidate@anestesiacarioca.com",
  "password": "123456"
}
```

### Response `200`

```json
{
  "token": "jwt-token-example",
  "user_id": 4821,
  "name": "QA Candidate"
}
```

### Response `401`

```json
{
  "error": "invalid_credentials"
}
```

## `GET /cart`

Retorna o carrinho atual do usuário autenticado.

### Response `200`

```json
{
  "cart_id": 9912,
  "items": [
    {
      "sku": "ANEST-001",
      "name": "Serviço A",
      "quantity": 1,
      "unit_price": 250
    }
  ],
  "subtotal": 250,
  "shipping": 20,
  "coupon": null,
  "total": 270
}
```

## `POST /cart/apply-coupon`

Aplica um cupom ao carrinho atual.

### Request

```json
{
  "coupon_code": "BEMVINDO10"
}
```

### Response `200`

```json
{
  "coupon_code": "BEMVINDO10",
  "discount_type": "percentage",
  "discount_value": 10,
  "discount_amount": 25,
  "total_before_discount": 250,
  "shipping": 20,
  "total_after_discount": 245
}
```

### Response `422`

```json
{
  "error": "invalid_coupon",
  "message": "Coupon is invalid or expired"
}
```

## `POST /checkout`

Fecha o pedido com base no carrinho atual.

### Request

```json
{
  "payment_method": "credit_card",
  "installments": 1
}
```

### Response `201`

```json
{
  "order_id": 55310,
  "status": "confirmed",
  "subtotal": 250,
  "shipping": 20,
  "discount": 25,
  "total": 245
}
```

## `GET /orders/{id}`

Retorna o pedido finalizado.

### Response `200`

```json
{
  "order_id": 55310,
  "status": "confirmed",
  "items": [
    {
      "sku": "ANEST-001",
      "quantity": 1,
      "unit_price": 250
    }
  ],
  "subtotal": 250,
  "shipping": 20,
  "discount": 25,
  "coupon_code": "BEMVINDO10",
  "total": 245
}
```

## Observações

- Considere autenticação por header `Authorization: Bearer <token>`.
- Considere que apenas um cupom pode ficar ativo por carrinho.
- Assuma que o cálculo final deve ser consistente entre carrinho, checkout e pedido persistido.
