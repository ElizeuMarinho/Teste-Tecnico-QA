# Teste Técnico - QA Pleno

## Contexto

Você está participando de um processo seletivo para a posição de `QA Pleno` na Anestesia Carioca.

Buscamos uma pessoa capaz de atuar com autonomia em cenários reais de qualidade, cobrindo:

- testes manuais
- testes de API
- raciocínio sobre automação
- investigação de bugs
- colaboração com desenvolvimento

O uso de IA generativa, incluindo `Codex`, `Claude Code` e ferramentas similares, está permitido. O critério principal deste teste não é volume de código, e sim a qualidade das decisões, a clareza do raciocínio e a consistência técnica da sua abordagem.

## Objetivo

Avaliar como você transforma requisitos em estratégia de testes, como prioriza cenários críticos e como investiga uma falha reportada em produção.

## Stack Sugerida

Você pode usar as ferramentas que considerar adequadas. Para manter aderência com a vaga, recomendamos:

- `Postman` ou similar para testes de API
- `JavaScript` para qualquer automação ou script auxiliar
- `Playwright` ou `Cypress`, se optar por automatizar parte do fluxo
- leitura básica de `PHP`, `SQL` e `GitHub Actions` no complemento técnico
- `Markdown` para documentar a resposta

## Tempo Esperado

`2h a 3h`

Não é necessário investir mais tempo do que isso. Priorização faz parte da avaliação.

Você não precisa entregar uma solução completa para todos os pontos. Queremos ver como você escolhe o que testar primeiro, o que automatizar agora e o que deixaria documentado para evolução.

## Cenário

O sistema possui uma área de gestão de pedidos. Uma nova funcionalidade foi entregue: permitir aplicar cupom de desconto no checkout.

### Regras de negócio

- O cupom pode conceder desconto percentual ou valor fixo.
- O cupom pode ter data de validade.
- O cupom pode estar ativo ou inativo.
- O desconto nunca pode resultar em total negativo.
- Apenas um cupom pode ser aplicado por pedido.
- O total final deve refletir corretamente subtotal, desconto e frete.
- O sistema deve registrar tentativa inválida de uso de cupom.

### Fluxo funcional esperado

1. O usuário faz login.
2. O usuário visualiza o carrinho.
3. O usuário aplica um cupom.
4. O checkout recalcula os totais.
5. O usuário conclui a compra.
6. O pedido fechado deve refletir os mesmos totais apresentados no checkout.

## API Disponível

Considere os endpoints abaixo como disponíveis:

- `POST /login`
- `GET /cart`
- `POST /cart/apply-coupon`
- `POST /checkout`
- `GET /orders/{id}`

Os detalhes de payload e exemplos estão em [../artifacts/api-spec.md](../artifacts/api-spec.md).

## Dados de Apoio

Utilize os dados em [../artifacts/test-data.json](../artifacts/test-data.json) como referência para construir seus cenários.

## Incidente Reportado

Um problema foi reportado em produção:

> Alguns usuários relatam que o cupom aparece como aplicado, mas o valor final no pedido fechado não bate com o valor exibido no checkout.

Detalhes adicionais do incidente estão em [../artifacts/bug-report.md](../artifacts/bug-report.md).

## Complemento Técnico

Além da estratégia de QA, queremos avaliar sua leitura técnica básica, compatível com a vaga.

Use o material em [../artifacts/technical-context.md](../artifacts/technical-context.md) e responda brevemente a `2` dos `3` pontos abaixo:

1. Aponte o risco principal no trecho de código `PHP` e como você validaria a correção.
2. Escreva ou descreva uma consulta `SQL` para encontrar pedidos com divergência entre total do carrinho e total do pedido.
3. Explique como incluiria uma regressão mínima em `GitHub Actions`.

Não esperamos uma implementação perfeita. O objetivo é entender seu raciocínio técnico e sua capacidade de colaborar com desenvolvimento.

## Sua Entrega

Envie sua resposta em um repositório ou arquivo compactado contendo:

1. `README.md` com a explicação geral da sua abordagem.
2. Casos de teste manuais para a funcionalidade.
3. Priorização dos cenários mais críticos, com justificativa.
4. Plano ou coleção de testes de API para os endpoints relevantes.
5. `1` ou `2` exemplos de automação em `JavaScript`, se você considerar que isso agrega valor.
6. Análise do bug reportado em produção.
7. Explicação do que você automatizaria agora, do que manteria manual e quais informações adicionais pediria ao time.
8. Resposta curta para `2` itens do complemento técnico.

Você pode organizar como preferir. Se quiser, use o template em [../examples/submission-template.md](../examples/submission-template.md).

## O Que Queremos Avaliar

- sua capacidade de transformar regra de negócio em teste
- sua habilidade de priorizar por risco
- sua clareza ao separar teste manual, teste de API e automação
- sua maturidade na investigação de bugs
- sua leitura técnica básica para colaborar com desenvolvimento
- sua objetividade ao justificar decisões

## Orientações Importantes

- Não queremos o maior número possível de cenários. Queremos os cenários certos.
- Se você usar IA, explicite onde ela ajudou e onde a decisão foi sua.
- Se fizer automação, priorize demonstrar critério e não volume de código.
- Se assumir algo que não está especificado, deixe a suposição explícita.

## Perguntas que sua resposta deve cobrir

1. Quais são os cenários mais importantes para validar essa funcionalidade?
2. Quais `10` cenários você executaria primeiro e por quê?
3. O que deveria ser validado em `API`, `UI`, `manual` e `automação`?
4. O que você automatizaria agora e o que deixaria manual neste momento?
5. Quais hipóteses explicam o bug de divergência de total?
6. Como você investigaria o incidente passo a passo?
7. Como você preveniria a regressão depois da correção?
8. Que evidência técnica você deixaria para ajudar o time de desenvolvimento a corrigir e monitorar o problema?

## Diferencial

Serão valorizadas respostas que demonstrem:

- critério de risco
- pensamento sistêmico
- boa comunicação técnica
- equilíbrio entre profundidade e pragmatismo
