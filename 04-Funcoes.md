# Funções Básicas em JavaScript

## 1. Introdução
Funções são blocos de código reutilizáveis que executam uma tarefa específica. Elas são fundamentais para organizar e estruturar seu código de forma eficiente.

## 2. Declaração de Funções

### 2.1 Sintaxe Básica
```javascript
function nomeDaFuncao() {
    // código a ser executado
}
```

### 2.2 Exemplo Prático
```javascript
function saudacao() {
    console.log("Olá! Bem-vindo ao estudo de funções!");
}

// Chamando a função
saudacao(); // Output: Olá! Bem-vindo ao estudo de funções!
```

### 2.3 Boas Práticas
- Use verbos para nomear funções (ex: calcular, obter, validar)
- Use camelCase para nomes de funções
- Mantenha funções pequenas e focadas em uma única responsabilidade
- Escolha nomes descritivos que indicam o que a função faz

## 3. Expressões de Função

### 3.1 Função Anônima
```javascript
const soma = function(a, b) {
    return a + b;
};

console.log(soma(5, 3)); // Output: 8
```

### 3.2 Arrow Function (ES6+)
```javascript
const multiplicar = (a, b) => a * b;

console.log(multiplicar(4, 2)); // Output: 8
```

### 3.3 Diferenças e Quando Usar
- Funções declaradas são hoisted (podem ser chamadas antes da declaração)
- Arrow functions são mais concisas e mantêm o this do contexto
- Use funções declaradas para métodos de objetos e construtores
- Use arrow functions para callbacks e funções simples

## 4. Parâmetros e Argumentos

### 4.1 Parâmetros Básicos
```javascript
function apresentar(nome, idade) {
    console.log(`Olá! Meu nome é ${nome} e tenho ${idade} anos.`);
}

apresentar("João", 25); // Output: Olá! Meu nome é João e tenho 25 anos.
```

### 4.2 Parâmetros Padrão
```javascript
function cumprimentar(nome = "visitante") {
    console.log(`Bem-vindo, ${nome}!`);
}

cumprimentar(); // Output: Bem-vindo, visitante!
cumprimentar("Maria"); // Output: Bem-vindo, Maria!
```

## 5. Return

### 5.1 Retornando Valores
```javascript
function calcularArea(base, altura) {
    return base * altura;
}

const area = calcularArea(5, 3);
console.log(area); // Output: 15
```

### 5.2 Retornos Múltiplos (usando objeto)
```javascript
function analisarNumero(num) {
    return {
        dobro: num * 2,
        quadrado: num ** 2,
        raizQuadrada: Math.sqrt(num)
    };
}

const analise = analisarNumero(4);
console.log(analise.dobro); // Output: 8
console.log(analise.quadrado); // Output: 16
```

## 6. Exercícios Práticos

### Exercício 1: Calculadora Básica
```javascript
/* 
Crie uma função chamada 'calculadora' que recebe três parâmetros:
- numero1 (number)
- numero2 (number)
- operacao (string: 'soma', 'subtracao', 'multiplicacao' ou 'divisao')
A função deve retornar o resultado da operação escolhida.
*/

// Sua solução aqui
```

### Exercício 2: Validador de Senha
```javascript
/*
Crie uma função que valide uma senha com os seguintes critérios:
- Mínimo de 8 caracteres
- Pelo menos uma letra maiúscula
- Pelo menos um número
- Retorne true se válida, false se inválida
*/

// Sua solução aqui
```

### Exercício 3: Conversor de Temperatura
```javascript
/*
Crie duas funções:
1. celsiusParaFahrenheit(celsius)
2. fahrenheitParaCelsius(fahrenheit)
Cada função deve retornar a temperatura convertida
*/

// Sua solução aqui
```

## 7. Soluções dos Exercícios

### Solução 1: Calculadora Básica
```javascript
function calculadora(numero1, numero2, operacao) {
    switch(operacao) {
        case 'soma':
            return numero1 + numero2;
        case 'subtracao':
            return numero1 - numero2;
        case 'multiplicacao':
            return numero1 * numero2;
        case 'divisao':
            if (numero2 === 0) return "Não é possível dividir por zero";
            return numero1 / numero2;
        default:
            return "Operação inválida";
    }
}

console.log(calculadora(10, 5, 'soma')); // Output: 15
console.log(calculadora(10, 5, 'divisao')); // Output: 2
```

### Solução 2: Validador de Senha
```javascript
function validarSenha(senha) {
    const temMinimo8Chars = senha.length >= 8;
    const temLetraMaiuscula = /[A-Z]/.test(senha);
    const temNumero = /[0-9]/.test(senha);
    
    return temMinimo8Chars && temLetraMaiuscula && temNumero;
}

console.log(validarSenha("Senha123")); // Output: true
console.log(validarSenha("senha123")); // Output: false (sem maiúscula)
```

### Solução 3: Conversor de Temperatura
```javascript
function celsiusParaFahrenheit(celsius) {
    return (celsius * 9/5) + 32;
}

function fahrenheitParaCelsius(fahrenheit) {
    return (fahrenheit - 32) * 5/9;
}

console.log(celsiusParaFahrenheit(0)); // Output: 32
console.log(fahrenheitParaCelsius(32)); // Output: 0
```

## 8. Dicas Finais e Boas Práticas

1. **Documentação**
   - Comente funções complexas
   - Use JSDoc para documentar parâmetros e retornos

2. **Organização**
   - Mantenha funções pequenas e focadas
   - Agrupe funções relacionadas
   - Evite efeitos colaterais

3. **Debuggando**
   - Use console.log() para depurar
   - Teste casos limite
   - Valide entradas quando necessário

4. **Performance**
   - Evite funções dentro de loops
   - Cache resultados de operações custosas
   - Otimize apenas quando necessário
