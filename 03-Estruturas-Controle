# Estruturas de Controle em JavaScript

## 1. Condicionais (if/else)

As estruturas condicionais permitem executar diferentes blocos de código baseados em condições.

### 1.1 Sintaxe Básica

```javascript
if (condição) {
    // código a ser executado se a condição for verdadeira
} else {
    // código a ser executado se a condição for falsa
}
```

### Exemplo Prático:
```javascript
function verificarIdade(idade) {
    if (idade >= 18) {
        return "Você é maior de idade";
    } else {
        return "Você é menor de idade";
    }
}

// Boas Práticas:
// 1. Use chaves {} mesmo em condições de uma linha
// 2. Mantenha condições simples e legíveis
// 3. Evite negações duplas
```

### 1.2 if/else if/else

```javascript
function classificarNota(nota) {
    if (nota >= 90) {
        return "A";
    } else if (nota >= 80) {
        return "B";
    } else if (nota >= 70) {
        return "C";
    } else {
        return "D";
    }
}
```

## 2. Switch

O switch é útil quando precisamos comparar uma expressão com múltiplos valores.

### Sintaxe:
```javascript
switch (expressão) {
    case valor1:
        // código
        break;
    case valor2:
        // código
        break;
    default:
        // código padrão
}
```

### Exemplo Prático:
```javascript
function obterDiaDaSemana(numero) {
    switch (numero) {
        case 1:
            return "Domingo";
        case 2:
            return "Segunda";
        case 3:
            return "Terça";
        case 4:
            return "Quarta";
        case 5:
            return "Quinta";
        case 6:
            return "Sexta";
        case 7:
            return "Sábado";
        default:
            return "Número inválido";
    }
}

// Boas Práticas:
// 1. Sempre use break para evitar fall-through não intencional
// 2. Inclua um caso default
// 3. Agrupe cases quando compartilham a mesma lógica
```

## 3. Operador Ternário

O operador ternário é uma forma concisa de escrever condicionais simples.

### Sintaxe:
```javascript
condição ? valor_se_verdadeiro : valor_se_falso
```

### Exemplo Prático:
```javascript
function parOuImpar(numero) {
    return numero % 2 === 0 ? "Par" : "Ímpar";
}

// Boas Práticas:
// 1. Use apenas para condições simples
// 2. Evite aninhar operadores ternários
// 3. Priorize legibilidade
```

## 4. Loops

### 4.1 For Loop

```javascript
// Contagem crescente
for (let i = 0; i < 5; i++) {
    console.log(i);
}

// Contagem decrescente
for (let i = 5; i > 0; i--) {
    console.log(i);
}
```

### 4.2 While Loop

```javascript
let contador = 0;
while (contador < 5) {
    console.log(contador);
    contador++;
}
```

### 4.3 Do-While Loop

```javascript
let numero = 1;
do {
    console.log(numero);
    numero++;
} while (numero <= 5);
```

## Exercícios Práticos

1. **Verificador de Números**
```javascript
/*
Crie uma função que recebe um número e retorna:
- "Positivo e Par" se for positivo e par
- "Positivo e Ímpar" se for positivo e ímpar
- "Negativo" se for negativo
- "Zero" se for zero
*/

// Solução:
function verificarNumero(num) {
    if (num === 0) {
        return "Zero";
    } else if (num > 0) {
        return num % 2 === 0 ? "Positivo e Par" : "Positivo e Ímpar";
    } else {
        return "Negativo";
    }
}
```

2. **Contador de Vogais**
```javascript
/*
Crie uma função que conta o número de vogais em uma string
usando um loop for e switch
*/

// Solução:
function contarVogais(texto) {
    let contador = 0;
    for (let i = 0; i < texto.length; i++) {
        switch (texto[i].toLowerCase()) {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                contador++;
                break;
        }
    }
    return contador;
}
```

3. **Tabuada**
```javascript
/*
Crie uma função que imprime a tabuada de um número
usando while loop
*/

// Solução:
function tabuada(numero) {
    let i = 1;
    while (i <= 10) {
        console.log(`${numero} x ${i} = ${numero * i}`);
        i++;
    }
}
```

## Boas Práticas Gerais

1. **Clareza e Legibilidade**
   - Mantenha o código indentado
   - Use nomes descritivos para variáveis e funções
   - Adicione comentários quando necessário

2. **Performance e Manutenção**
   - Evite loops infinitos
   - Use break e continue apropriadamente
   - Prefira for quando souber o número de iterações
   - Use while quando a condição de parada for dinâmica

3. **Estruturação**
   - Evite muitos níveis de aninhamento
   - Considere extrair lógica complexa para funções separadas
   - Mantenha condições simples e claras

4. **Testes**
   - Sempre teste valores limite
   - Considere casos extremos (números negativos, zero, strings vazias)
   - Verifique todos os caminhos possíveis do código
