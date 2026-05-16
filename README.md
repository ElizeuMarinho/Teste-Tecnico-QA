# Teste Técnico QA

## 1. Visão Geral

- Como entendi o problema

O problema apresentado trata-se de uma inconsistência nos valores do checkout (fechamento do pedido), em que um cupom de desconto é aplicado, mas os valores calculados não correspondem ao esperado, resultando em um total incorreto.
Essa falha pode impactar diretamente as receitas da empresa, além de comprometer a confiança do usuário no processo de compra. Ao identificar valores inconsistentes durante o fechamento do pedido, o cliente pode não se sentir seguro para concluir a compra, afetando negativamente tanto a experiência do usuário quanto a reputação da empresa.

- Principais riscos

Os principais riscos estão relacionados à exibição de valores cobrados incorretamente, o que pode afastar usuários ao transmitir a percepção de que a plataforma não é confiável. Esse problema pode ser causado pela ausência de testes adequados e de um processo eficiente de validação do produto antes de sua disponibilização em produção.

- Suposições adotadas

Supõe-se que, ao utilizar a plataforma e inserir um cupom de desconto, o usuário receba como retorno o valor total com a aplicação correta do desconto, garantindo que o cupom seja aplicado apenas uma única vez e que o valor final apresentado esteja correto.

## 2. Casos de Teste Manuais

Liste os cenários mais relevantes e descreva:

1 - Validação de Interface.

- objetivo

  Garantir que a interface do checkout esteja disponível e os campos estejam visíveis para preenchimento de cupom e conclusão de compra.

- pré-condições

  Produto estar adicionado ao carrinho durante o processo de finalizar compra.

- passos

  1 - Acessar opção Carrinho
  2 - Validar valores apresentado em tela
  3 - Validar se campo cupom está disponível para preenchimento.
  4 - Validar se botão finalizar compra está disponível.

- resultado esperado

  Elementos disponíveis em tela apresentando as informações de produto e valores corretamente.

- prioridade

  0

2 - Validação de Produtos adicionado no carrinho.

- objetivo

  Garantir que os produtos selecionados no processo de navegação do site estejam devidamente adicionados ao carrinho com seus valores e informações.

- pré-condições

  Produto estar disponível na loja e ter sido selecionado pelo usuário para ser adicionado ao carrinho.

- passos

  1 - Acessar opção Carrinho
  2 - Validar Nome dos Itens do carrinho
  3 - Validar Valores dos itens
  4 - Validar quantidades.

- resultado esperado

  Os produtos adicionados precisam ser condizentes com o que o usuário selecionou durante sua navegação.

- prioridade

  1

3 - Validação de Valor de total da compra.

- objetivo

  Garantir que o valor calculado e apresentado no final condiz com o valor total esperado

- pré-condições

  Usuário já autenticado e com produtos em seu carinho para finalização de compra.

- passos

  1 - Acessar opção Carrinho
  2 - Validar Valor de subtotal
  3 - Validar Valores de descontos
  4 - Validar Total.

- resultado esperado

  Os valores precisam estar condizentes com as informações inseridas, como produtos e cupom.

- prioridade

  1

4 - Validação de funcionamento do cupom

- objetivo

  Garantir que o valor apresentado condiz com o cupom utilizado

- pré-condições

  Usuário já autenticado e com produtos em seu carinho para finalização de compra com cupom válido.

- passos

  1 - Acessar opção Carrinho
  2 - Validar campo de inserção de cupom
  3 - Inserir cupom válido
  4 - Validar valor de desconto.

- resultado esperado

  Os valores precisam estar condizentes com as informações inseridas, como produtos e cupom.

- prioridade

  1

## 3. Priorização

Informe quais `10` cenários executaria primeiro e por quê.

Os cenários automatizados que envolvem a API em suas condições de sucesso, garantindo o funcionamento da API e tendo os valores corretos para então serem utilizados na plataforma onde o usuário atuará validando login, informações de carrinho, aplicação de cupom, checkout (pagamento) e geração de ordem, em seguida validação de UI para garantir que os elementos estão disponíveis para uso na visão do usuário, validação de valores de cupom na UI, verificando se os cupons condizem com o valor esperado, validação de total de compra UI, para validar se as informações que são apresentadas na API também estão corretamente sendo executadas nos elementos da página, garantindo que não há algum erro de implementação em alguns dos elementos da página que possa causar algum erro e finalização de compra utilizando a interface de usuário.

## 4. Testes de API

Descreva:

- endpoints cobertos

A API é organizada em endpoints para realização de login, visualização do carrinho, aplicação de cupom, fechamento de pedido e retorno de pedido. Dessa forma, é possível acompanhar o fluxo completo de ponta a ponta no processo de compra.
A autenticação é realizada por meio de um token gerado no login, utilizado para validação das requisições subsequentes. Assim, é necessário que o usuário esteja previamente autenticado para executar qualquer ação relacionada ao processo de compra.

- cenários positivos e negativos

Os principais cenários estão implementados nos endpoints; no entanto, alguns fluxos de erro não estão devidamente tratados. Isso pode levar o usuário a encontrar falhas sem uma resposta clara e documentada, dificultando a compreensão do que ocorreu durante a navegação.
Por outro lado, nos cenários de sucesso, como respostas 200 e 201, as informações são claras e bem definidas. Contudo, nos cenários negativos, nem todos os possíveis erros estão mapeados.
Como exemplo, não está claramente definido o retorno em casos como uma requisição sem autenticação ao buscar um recurso, a consulta de um id inexistente no endpoint orders/{id}, ou ainda falhas durante o processamento de pagamento no POST /checkout sendo pagamento não aprovado ou até mesmo um checkout com carrinho vazio ao verificar o GET /cart.
Essas lacunas podem comprometer a previsibilidade da API e a experiência do usuário ao lidar com situações de erro.

- validações de status code

Os códigos HTTP configurados seguem um padrão que esclarece os erros encontrados e fornece informações claras sobre como eles podem ser corrigidos, permitindo que o usuário compreenda a situação e consiga concluir suas etapas, finalizando a compra com sucesso.

- validações de contrato e regra de negócio

Visando o objetivo final do processo de compra, é importante garantir que as respostas da API proporcionem uma melhor experiência ao usuário, respeitando as regras de negócio estabelecidas.
Isso inclui assegurar que o cupom de desconto seja utilizado apenas uma vez por compra, a utilização de um formato adequado para valores monetários, o impedimento de checkout com carrinho vazio, a validação do pagamento e a garantia de cálculo correto quando um cupom é aplicado.
Também é necessário impedir a realização de pedidos sem autenticação e atualizar os valores do carrinho sempre que houver alterações.
Além disso, devem ser consideradas as validações de contrato, que envolvem o uso de códigos HTTP condizentes com cada tipo de erro, a definição de campos obrigatórios no payload, a validação da estrutura dos dados e a padronização das respostas da API.

## 5. Automação

Se optar por automatizar:

- diga por que escolheu esses cenários

O cenário apresenta um fluxo E2E (end-to-end) do processo de finalização de compra com aplicação de cupom. Dessa forma, é possível verificar e validar todo o fluxo, garantindo que o caminho de sucesso esteja de acordo com o comportamento esperado e com a regra de negócio definida.

- explique por que não automatizou os demais

Os demais cenários, por se tratarem de possíveis fluxos de erro, devem ser executados manualmente para permitir uma análise mais detalhada e aprofundada. Isso possibilita identificar comportamentos fora do fluxo padrão, validar ações alternativas do usuário e detectar eventuais falhas que não estejam cobertas pelo caminho de sucesso.

- código em `JavaScript` utilizando Playwright

```javascript
import { test, expect, request } from '@playwright/test';

test('Fluxo completo de checkout - login até criação de pedido', async () => {
  const apiContext = await request.newContext({
    baseURL: 'https://sua-api.com',
  });

  /**
   * 1. LOGIN
   */
  const loginResponse = await apiContext.post('/login', {
    data: {
      email: 'qa.candidate@anestesiacarioca.com',
      password: '123456',
    },
  });

  expect(loginResponse.status()).toBe(200);

  const loginBody = await loginResponse.json();
  const token = loginBody.token;

  expect(token).toBeTruthy();

  /**
   * 2. HEADERS AUTENTICADOS
   */
  const authContext = await request.newContext({
    baseURL: 'https://sua-api.com',
    extraHTTPHeaders: {
      Authorization: `Bearer ${token}`,
    },
  });

  /**
   * 3. GET CART
   */
  const cartResponse = await authContext.get('/cart');

  expect(cartResponse.status()).toBe(200);

  const cart = await cartResponse.json();

  expect(cart.items.length).toBeGreaterThan(0);

  const initialTotal = cart.total;

  /**
   * 4. APPLY COUPON
   */
  const couponResponse = await authContext.post('/cart/apply-coupon', {
    data: {
      coupon_code: 'DESCONTO10',
    },
  });

  expect(couponResponse.status()).toBe(200);

  const cartWithCoupon = await couponResponse.json();

  expect(cartWithCoupon).toHaveProperty('discount');
  expect(cartWithCoupon.total).toBeLessThanOrEqual(initialTotal);

  /**
   * 5. CHECKOUT
   */
  const checkoutResponse = await authContext.post('/checkout', {
    data: {
      cart_id: cart.cart_id,
      payment_method: 'credit_card',
    },
  });

  expect(checkoutResponse.status()).toBe(201);

  const checkout = await checkoutResponse.json();

  expect(checkout).toHaveProperty('order_id');
  expect(checkout.status).toBe('confirmed');

  /**
   * 6. VALIDAR PEDIDO FINAL
   */
  const orderResponse = await authContext.get(`/orders/${checkout.order_id}`);

  expect(orderResponse.status()).toBe(200);

  const order = await orderResponse.json();

  expect(order.total).toBeDefined();
  expect(order.cart_id).toBe(cart.cart_id);
  expect(order.status).toBe('confirmed');
});
```

## 6. Análise do Bug

Descreva:

- hipóteses principais

H1 - O cupom é válido no sistema e atende às regras de negócio?
H2 - A API de aplicação de cupom está funcionando corretamente em todos os cenários?
H3 - O cálculo de finalização de compra está sendo executado corretamente e de forma consistente entre carrinho e pedido?

- passos de investigação

1 - Buscar logs de erros.
2 - Validar se o cupom é valido e está registrado com valor correto;
3 - Verificar se o valor de cupom é registrado no banco de dados na ordem e no carrinho;
4 - Verificar divergência de valores entre ordem e carrinho;
5 - Validar se API está funcionando corretamente quando executada o endpoint apply-coupon;
6 - Validar código associado ao botão finalizar compra;

- impacto

A presença de um bug em produção pode impactar diretamente o fluxo de caixa de uma empresa, uma vez que afeta a reputação e a confiança dos usuários em relação à plataforma. Isso pode resultar na redução do número de compras realizadas no site, no aumento de solicitações de estorno e em uma maior demanda de acionamentos ao suporte.

- prevenção de regressão

Implementar processos claros de revisão de código e testes, garantindo que erros anteriormente identificados não voltem a ocorrer. Para isso, é fundamental realizar a análise de causa raiz, com o objetivo de compreender a origem do problema e, a partir disso, implementar melhorias e controles adequados que assegurem maior qualidade no produto final.
Além disso, é importante alinhar com o time de desenvolvimento padrões de qualidade, de forma a manter um fluxo contínuo de desenvolvimento e validação de funcionalidades, prevenindo que defeitos cheguem à produção.

## 7. Uso de IA

Explique brevemente:

- quais ferramentas usou

ChatGPT

- onde elas ajudaram

Escrita de código para os testes automatizados, de forma a acelerar o desenvolvimento dos testes.

- quais decisões finais foram suas

Foi elaborado um prompt estruturado com base nas informações fornecidas da API, incluindo a definição da linguagem de programação utilizada. Após a geração do código, foi realizada uma revisão técnica, com ajustes nos endpoints e validações adicionais de regras de negócio e contrato.
Esse processo teve como objetivo garantir uma cobertura mais eficiente dos cenários de teste, bem como a consistência e qualidade da implementação automatizada.

## 8. Complemento Técnico

Responda `2` dos `3` itens:

- análise do trecho `PHP`

Analisando a estrutura do código, é possível notar que não há uma validação para verificar se existe ou não um código de cupom durante o cálculo do total. Atualmente, apenas é retornada a presença do cupom ou um valor nulo.
Para que a lógica funcione corretamente, seria necessária uma validação condicional: caso o cupom esteja preenchido e seja válido, o cálculo do total deve considerar o valor do desconto aplicado; caso contrário, o total deve ser calculado sem levar em consideração qualquer desconto de cupom.
Além disso, também são necessários ajustes e cuidados relacionados ao tratamento de valores negativos, bem como à utilização de variáveis adequadas ou bibliotecas específicas para operações monetárias, garantindo maior precisão nos cálculos financeiros.

- consulta ou estratégia `SQL`

Para identificar divergências de valores, foi considerada a utilização de um JOIN para o cruzamento de dados entre as tabelas, utilizando o cart_id como chave de referência. Dessa forma, é possível comparar os valores totais registrados no carrinho e na ordem, verificando se há consistência entre eles.
Na consulta apresentada, caso não existam divergências, os registros são retornados normalmente. Por outro lado, caso haja inconsistências, nenhum resultado será retornado. Para realizar a verificação inversa, basta substituir o operador de igualdade = pelo operador de diferença <>.

```SQL
SELECT o.user_id, o.cart_id, o.total, ct.total FROM orders o
    INNER JOIN cart_totals ct
        ON o.cart_id = ct.cart_id
    WHERE o.total = ct.total;
```

- proposta de regressão em `GitHub Actions`
