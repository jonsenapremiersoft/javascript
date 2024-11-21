# Debug e Depuração

## 1. Conceitos Básicos de Debug

### O que é Debug?
Debug (ou depuração) é o processo de identificar e corrigir erros no código. É uma habilidade essencial para qualquer desenvolvedor.

### Por que debugar?
- Encontrar bugs
- Entender o fluxo do código
- Otimizar performance
- Melhorar a qualidade do código

## 2. Console e Métodos de Debug

### console.log()
```javascript
// Uso básico
console.log("Mensagem simples");

// Múltiplos valores
console.log("Nome:", nome, "Idade:", idade);

// Com template strings
console.log(`Usuario ${usuario} logado`);
```

### Outros métodos do console
```javascript
// Mensagem de erro
console.error("Erro crítico!");

// Mensagem de aviso
console.warn("Atenção: valor inválido");

// Mensagem informativa
console.info("Processo iniciado");

// Tabela de dados
const usuarios = [
    { nome: "Ana", idade: 25 },
    { nome: "João", idade: 30 }
];
console.table(usuarios);

// Tempo de execução
console.time("minhaOperacao");
// ... código ...
console.timeEnd("minhaOperacao");
```

## 3. Breakpoints e DevTools

### Como usar o DevTools
1. Abra o DevTools (F12 ou Ctrl+Shift+I)
2. Vá para a aba "Sources"
3. Localize seu arquivo JavaScript
4. Clique na linha onde deseja adicionar o breakpoint

### Tipos de Breakpoints
```javascript
function calcularMedia(notas) {
    // Breakpoint de linha
    let soma = 0;
    
    // Breakpoint condicional
    for(let nota of notas) {
        if (nota < 0) debugger; // Pausa se nota for negativa
        soma += nota;
    }
    
    return soma / notas.length;
}
```

## 4. Tipos Comuns de Erros

### Erros de Sintaxe
```javascript
// Erro: falta de fechamento de parênteses
if (x === 5 {
    console.log("x é 5");
}

// Correção
if (x === 5) {
    console.log("x é 5");
}
```

### Erros de Referência
```javascript
// Erro: variável não definida
console.log(minhaVariavel);

// Correção
let minhaVariavel = "valor";
console.log(minhaVariavel);
```

### Erros de Tipo
```javascript
// Erro: operação com tipos incompatíveis
const numero = "5";
const resultado = numero + 2; // "52"

// Correção
const numero = parseInt("5");
const resultado = numero + 2; // 7
```

## 5. Técnicas Avançadas de Depuração

### Try-Catch
```javascript
try {
    // Código que pode gerar erro
    const resultado = funcaoPerigosa();
} catch (erro) {
    console.error("Erro capturado:", erro.message);
    // Tratamento do erro
} finally {
    // Código executado sempre
    console.log("Processo finalizado");
}
```

### Custom Error
```javascript
class ValidacaoError extends Error {
    constructor(mensagem) {
        super(mensagem);
        this.name = "ValidacaoError";
    }
}

function validarIdade(idade) {
    if (idade < 0) {
        throw new ValidacaoError("Idade não pode ser negativa");
    }
    return true;
}
```

## 6. Debugger Statement

### O que é o debugger
O `debugger` é uma declaração que pausa a execução do código no ponto onde é inserido, permitindo inspeção detalhada do estado do programa.

### Como usar
```javascript
function calcularSalario(horasTrabalhadas, valorHora) {
    debugger; // O código pausa aqui quando DevTools está aberto
    const salarioBase = horasTrabalhadas * valorHora;
    
    if (horasTrabalhadas > 40) {
        debugger; // Pausa para verificar horas extras
        const horasExtras = horasTrabalhadas - 40;
        return salarioBase + (horasExtras * valorHora * 1.5);
    }
    
    return salarioBase;
}
```

### Vantagens do debugger
- Pausa automática da execução
- Permite inspeção de variáveis locais
- Possibilidade de execução passo a passo
- Avaliação de expressões no console durante a pausa

### Uso com condicionais
```javascript
let contador = 0;

function processar() {
    contador++;
    if (contador > 10) {
        debugger; // Só pausa após 10 iterações
    }
    // resto do código
}
```

## 7. Exercícios Práticos

### Exercício 1: Debugando uma Função
```javascript
// Encontre e corrija os erros nesta função
function calcularDesconto(preco, percentual) {
    const desconto = preco * (percentual / 100;
    return preco - desconto;
}
```

### Exercício 2: Tratamento de Erros
```javascript
// Implemente tratamento de erros adequado
function dividir(a, b) {
    // Seu código aqui
    // Deve lançar erro se b for zero
    // Deve validar se os parâmetros são números
}
```

### Exercício 3: Debug com Console
```javascript
// Use diferentes métodos do console para depurar
function processarDados(dados) {
    // Seu código aqui
    // Use console.time para medir performance
    // Use console.table para visualizar dados
    // Use console.error para erros
}
```





## Dicas Finais
1. Sempre verifique o console do navegador
2. Use breakpoints estrategicamente
3. Faça log de valores importantes
4. Teste diferentes cenários
5. Documente os bugs encontrados

## Recursos Adicionais
- [MDN Web Docs - Debugging JavaScript](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Debugging)
- [Chrome DevTools Documentation](https://developers.google.com/web/tools/chrome-devtools)
