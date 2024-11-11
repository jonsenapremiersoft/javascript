# Desafio: Calculadora de Conta de Restaurante 🍽️

## Contexto
Você foi contratado para desenvolver uma solução para um restaurante que precisa de um programa para auxiliar no cálculo das contas dos clientes. O programa deve calcular o valor total da conta, incluindo a gorjeta sugerida, e também ser capaz de dividir a conta entre várias pessoas.

## Requisitos Funcionais

1. Crie uma função chamada `calcularConta` que receba os seguintes parâmetros:
   - valorConsumido (número positivo representando o valor total consumido)
   - numeroPessoas (número inteiro positivo representando quantidade de pessoas)
   - qualidadeServico (string indicando a qualidade do serviço)

2. A função deve incluir as seguintes regras para gorjeta baseadas na qualidade do serviço:
   - "excelente" → 15% de gorjeta
   - "bom" → 10% de gorjeta
   - "regular" → 5% de gorjeta

3. A função deve realizar as seguintes validações:
   - O valor consumido deve ser maior que zero
   - O número de pessoas deve ser maior que zero
   - A qualidade do serviço deve ser uma das três opções válidas

4. A função deve retornar um objeto contendo:
   - Valor do consumo
   - Valor da gorjeta sugerida
   - Valor total (consumo + gorjeta)
   - Valor por pessoa
   - Número de pessoas

5. Todos os valores monetários devem ser formatados com duas casas decimais

## Requisitos Técnicos

- Utilize variáveis com nomes claros e significativos
- Implemente estruturas condicionais (if/else) para validações
- Use estrutura switch/case para definir a porcentagem da gorjeta
- Aplique operadores matemáticos para os cálculos necessários
- Documente seu código com comentários explicativos
- Crie pelo menos 3 exemplos de uso com diferentes cenários

## Exemplo de Saída Esperada
```javascript
// Exemplo de chamada da função:
calcularConta(120.00, 3, "excelente")

// Deve retornar um objeto como este:
{
    consumo: 120.00,
    gorjetaSugerida: 18.00,
    valorTotal: 138.00,
    valorPorPessoa: 46.00,
    numeroPessoas: 3
}
```

## Desafios Extras (Opcionais)
Para quem quiser se desafiar ainda mais, implemente:
1. Validação para valor máximo por pessoa (até R$ 1000,00)
2. Desconto de 5% para grupos com mais de 5 pessoas
3. Opção de gorjeta personalizada (um valor percentual informado pelo usuário)
4. Mensagem personalizada quando o valor por pessoa for maior que R$ 100,00


## Dicas
- Teste sua função com diferentes valores
- Verifique se todas as validações estão funcionando
- Confira se os cálculos matemáticos estão precisos
- Garanta que o código está tratando corretamente os números decimais

Boa sorte! 🚀
