# Objeto Math

## Introdução

O objeto Math é uma ferramenta fundamental em JavaScript que nos permite realizar operações matemáticas complexas. Diferente de outros objetos, não precisamos criar uma instância - ele já está disponível globalmente no JavaScript.

## Constantes Matemáticas Importantes

```javascript
// PI - A famosa constante matemática π
console.log(Math.PI); // 3.141592653589793

// Número de Euler (e)
console.log(Math.E); // 2.718281828459045
```

Exemplo prático com PI:
```javascript
// Calculando a circunferência de uma pizza
const diametroPizza = 35; // cm
const circunferencia = Math.PI * diametroPizza;
console.log(`Uma pizza de ${diametroPizza}cm de diâmetro tem ${circunferencia.toFixed(2)}cm de circunferência`);
```

## Arredondamento de Números

```javascript
// Math.round() - Arredonda para o inteiro mais próximo
const mediaDeVendas = 87.4;
console.log(Math.round(mediaDeVendas)); // 87

// Math.ceil() - Arredonda para cima
const pessoasNaFila = 45.1;
console.log(Math.ceil(pessoasNaFila)); // 46 (precisamos de cadeiras suficientes!)

// Math.floor() - Arredonda para baixo
const litrosDeLeite = 2.8;
console.log(Math.floor(litrosDeLeite)); // 2 (litros completos)

// Math.trunc() - Remove a parte decimal
const temperaturaAtual = 23.7;
console.log(Math.trunc(temperaturaAtual)); // 23
```

## Encontrando Valores Máximos e Mínimos

```javascript
// Math.max() - Encontra o maior valor
const temperaturaSemana = [22, 24, 28, 19, 23];
const maiorTemperatura = Math.max(...temperaturaSemana);
console.log(`A temperatura mais alta da semana foi ${maiorTemperatura}°C`);

// Math.min() - Encontra o menor valor
const precoProduto = [45.99, 39.99, 42.99, 49.99];
const menorPreco = Math.min(...precoProduto);
console.log(`O menor preço encontrado foi R$ ${menorPreco}`);
```

## Potência e Raiz Quadrada

```javascript
// Math.pow() - Calcula potência
const areaQuadrado = Math.pow(5, 2); // 5²
console.log(`A área do quadrado é ${areaQuadrado}m²`);

// Math.sqrt() - Calcula raiz quadrada
const hipotenusa = Math.sqrt(Math.pow(3, 2) + Math.pow(4, 2));
console.log(`A hipotenusa do triângulo é ${hipotenusa}`);
```

## Números Aleatórios

```javascript
// Math.random() - Gera número aleatório entre 0 e 1
// Gerando número entre 1 e 100
const numeroSorteado = Math.floor(Math.random() * 100) + 1;
console.log(`Número sorteado: ${numeroSorteado}`);

// Simulando dado de 6 faces
const resultadoDado = Math.floor(Math.random() * 6) + 1;
console.log(`Você tirou ${resultadoDado} no dado!`);
```

## Funções Trigonométricas

```javascript
// Calculando altura de um objeto usando ângulo
const distanciaBase = 20; // metros
const angulo = 45; // graus
const anguloRadianos = angulo * Math.PI / 180;
const altura = distanciaBase * Math.tan(anguloRadianos);
console.log(`A altura do objeto é aproximadamente ${altura.toFixed(2)} metros`);

// Calculando distância entre dois pontos
const x1 = 0, y1 = 0; // Ponto A
const x2 = 3, y2 = 4; // Ponto B
const distancia = Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
console.log(`A distância entre os pontos é ${distancia} unidades`);
```

## Valor Absoluto

```javascript
// Math.abs() - Retorna o valor absoluto
const saldoBancario = -150;
const valorDevido = Math.abs(saldoBancario);
console.log(`Você precisa depositar R$ ${valorDevido} para zerar sua conta`);

// Calculando diferença de temperatura
const tempManha = 18;
const tempTarde = 25;
const variacaoTemperatura = Math.abs(tempManha - tempTarde);
console.log(`A temperatura variou ${variacaoTemperatura}°C durante o dia`);
```

## Conclusão

O objeto Math é uma ferramenta poderosa que nos permite realizar desde cálculos simples até operações matemáticas complexas. Seus métodos são especialmente úteis em:
- Cálculos financeiros
- Jogos
- Visualização de dados
- Análises científicas
- Processamento de sinais
- Geometria computacional

Lembre-se que todos os métodos do Math retornam números em ponto flutuante (exceto os métodos de arredondamento quando retornam inteiros), e trabalham com o padrão IEEE 754 para aritmética de ponto flutuante.
