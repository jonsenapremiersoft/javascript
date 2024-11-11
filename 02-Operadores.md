# Operadores em JavaScript

## 1. Operadores Aritméticos

Os operadores aritméticos realizam operações matemáticas básicas.

### Principais Operadores:
* `+` (Adição)
* `-` (Subtração)
* `*` (Multiplicação)
* `/` (Divisão)
* `%` (Módulo/Resto)
* `**` (Exponenciação)
* `++` (Incremento)
* `--` (Decremento)

### Exemplos:
```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.3333...
console.log(a % b);  // 1
console.log(a ** b); // 1000

// Incremento e Decremento
let contador = 1;
contador++; // contador = 2
contador--; // contador = 1
```

### ⚠️ Boa Prática:
* Sempre use parênteses para deixar clara a ordem das operações
* Evite usar incremento/decremento em expressões complexas

## 2. Operadores de Comparação

Operadores de comparação retornam valores booleanos (true/false).

### Principais Operadores:
* `==` (Igual a - compara valor)
* `===` (Estritamente igual - compara valor e tipo)
* `!=` (Diferente de - compara valor)
* `!==` (Estritamente diferente - compara valor e tipo)
* `>` (Maior que)
* `<` (Menor que)
* `>=` (Maior ou igual)
* `<=` (Menor ou igual)

### Exemplos:
```javascript
let x = 5;
let y = "5";

console.log(x == y);   // true (compara apenas valor)
console.log(x === y);  // false (compara valor e tipo)
console.log(x != y);   // false
console.log(x !== y);  // true

console.log(x > 3);    // true
console.log(x < 3);    // false
console.log(x >= 5);   // true
console.log(x <= 4);   // false
```

### ⚠️ Boa Prática:
* Sempre use `===` e `!==` ao invés de `==` e `!=`
* Evite comparações implícitas

## 3. Operadores Lógicos

Operadores lógicos são usados para combinar condições.

### Principais Operadores:
* `&&` (AND lógico)
* `||` (OR lógico)
* `!` (NOT lógico)

### Exemplos:
```javascript
let idade = 25;
let temCarteira = true;

// AND (&&) - todas as condições devem ser verdadeiras
console.log(idade >= 18 && temCarteira); // true

// OR (||) - pelo menos uma condição deve ser verdadeira
let temDinheiro = false;
console.log(temDinheiro || temCarteira); // true

// NOT (!) - inverte o valor booleano
console.log(!temCarteira); // false
```

### ⚠️ Boa Prática:
* Use parênteses para deixar clara a ordem das operações lógicas
* Evite operadores lógicos aninhados demais

## Exercícios

1. **Calculadora Básica**
```javascript
// Crie uma função que receba dois números e um operador (+, -, *, /) 
// e retorne o resultado da operação

function calculadora(num1, num2, operador) {
    // Implemente aqui
}

// Teste: calculadora(10, 5, '+') deve retornar 15
```

2. **Verificador de Idade**
```javascript
// Crie uma função que verifique se uma pessoa pode dirigir
// Condições: Idade >= 18 E ter carteira de motorista

function podeDigirir(idade, temCarteira) {
    // Implemente aqui
}

// Teste: podeDigirir(20, true) deve retornar true
```

3. **Comparador de Números**
```javascript
// Crie uma função que compare dois números e retorne:
// "Maior" se o primeiro for maior
// "Menor" se o primeiro for menor
// "Igual" se forem iguais

function compararNumeros(num1, num2) {
    // Implemente aqui
}

// Teste: compararNumeros(5, 3) deve retornar "Maior"
```

## Resoluções dos Exercícios

1. **Calculadora Básica**
```javascript
function calculadora(num1, num2, operador) {
    switch(operador) {
        case '+': return num1 + num2;
        case '-': return num1 - num2;
        case '*': return num1 * num2;
        case '/': return num2 !== 0 ? num1 / num2 : "Erro: divisão por zero";
        default: return "Operador inválido";
    }
}
```

2. **Verificador de Idade**
```javascript
function podeDigirir(idade, temCarteira) {
    return idade >= 18 && temCarteira;
}
```

3. **Comparador de Números**
```javascript
function compararNumeros(num1, num2) {
    if (num1 > num2) return "Maior";
    if (num1 < num2) return "Menor";
    return "Igual";
}
```

## Resumo das Boas Práticas

1. **Operadores Aritméticos**
   * Use parênteses para clareza
   * Evite operações muito complexas em uma única linha
   * Cuidado com operações que podem gerar NaN ou Infinity

2. **Operadores de Comparação**
   * Prefira sempre `===` e `!==`
   * Evite comparações implícitas
   * Teste casos limite nas comparações

3. **Operadores Lógicos**
   * Use parênteses para deixar clara a precedência
   * Quebre expressões muito complexas em variáveis intermediárias
   * Aproveite o short-circuit evaluation do && e ||
