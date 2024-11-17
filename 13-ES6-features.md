# Features Modernas do JavaScript (ES6+)

## Sumário
1. [Modules (import/export)](#1-modules-importexport)
2. [Template Literals](#2-template-literals)
3. [Spread/Rest Operators](#3-spreadrest-operators)
4. [Destructuring Avançado](#4-destructuring-avançado)
5. [Null Coalescing](#5-null-coalescing)

## 1. Modules (import/export)

### O que são?
Modules são unidades de código reutilizáveis que nos permitem organizar nosso código em arquivos separados. Pense neles como "capítulos" de um livro - cada um com sua responsabilidade específica.

### Benefícios
- ✅ Código mais organizado e manutenível
- ✅ Reutilização de código
- ✅ Melhor encapsulamento
- ✅ Facilidade para testes
- ✅ Carregamento sob demanda

### Sintaxe Básica

#### Exportando
```javascript
// arquivo: mathUtils.js

// Exportações nomeadas
export const sum = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// Export default (só pode ter um por arquivo)
export default class Calculator {
  // implementação
}
```

#### Importando
```javascript
// arquivo: main.js
import Calculator, { sum, subtract } from './mathUtils.js';

// Importando tudo como um objeto
import * as MathUtils from './mathUtils.js';
```

### Exemplo Prático: Sistema de E-commerce
```javascript
// arquivo: productService.js
export class ProductService {
  static async getProducts() {
    // lógica para buscar produtos
  }
  
  static async saveProduct(product) {
    // lógica para salvar produto
  }
}

// arquivo: checkout.js
import { ProductService } from './productService.js';

const products = await ProductService.getProducts();
```

## 2. Template Literals

### O que são?
Template literals são strings melhoradas que permitem interpolação de expressões e múltiplas linhas de forma elegante.

### Benefícios
- ✅ Strings multilinhas sem caracteres especiais
- ✅ Interpolação de expressões
- ✅ Melhor legibilidade
- ✅ Menos erros de concatenação

### Sintaxe e Exemplos

#### Exemplo Básico
```javascript
const nome = 'Maria';
const idade = 30;

// Forma antiga
const mensagem1 = 'Olá ' + nome + ', você tem ' + idade + ' anos.';

// Com template literals
const mensagem2 = `Olá ${nome}, você tem ${idade} anos.`;
```

#### Exemplo Prático: Sistema de Notificações
```javascript
const usuario = {
  nome: 'Maria',
  ultimaCompra: {
    produto: 'Notebook',
    valor: 3500
  }
};

const notificacao = `
  Olá ${usuario.nome},
  
  Sua compra do ${usuario.ultimaCompra.produto}
  no valor de R$${usuario.ultimaCompra.valor} foi confirmada!
  
  Agradecemos a preferência!
`;
```

#### Geração de HTML Dinâmico
```javascript
const gerarCardProduto = (produto) => `
  <div class="card">
    <h3>${produto.nome}</h3>
    <p class="preco">R$${produto.preco.toFixed(2)}</p>
    ${produto.emEstoque 
      ? '<span class="disponivel">Em estoque</span>' 
      : '<span class="indisponivel">Indisponível</span>'
    }
  </div>
`;
```

## 3. Spread/Rest Operators

### O que são?
O operador `...` tem duas funcionalidades principais:
- **Spread**: "Espalha" elementos de um array ou objeto
- **Rest**: "Agrupa" elementos em um array

### Spread Operator

#### Com Arrays
```javascript
// Combinando arrays
const frutas = ['maçã', 'banana'];
const vegetais = ['cenoura', 'brócolis'];
const alimentos = [...frutas, ...vegetais];

// Copiando arrays
const frutasOriginais = ['maçã', 'banana'];
const frutasCopia = [...frutasOriginais];
```

#### Com Objetos
```javascript
const dadosPessoais = {
  nome: 'João',
  email: 'joao@email.com'
};

const endereço = {
  cidade: 'São Paulo',
  bairro: 'Centro'
};

const usuarioCompleto = {
  ...dadosPessoais,
  ...endereço,
  dataCadastro: new Date()
};
```

### Rest Operator

#### Em Funções
```javascript
// Função que aceita quantidade ilimitada de argumentos
const somarTodos = (...numeros) => {
  return numeros.reduce((total, num) => total + num, 0);
};

somarTodos(1, 2, 3, 4, 5); // 15

// Coletando parâmetros extras
function registrarVenda(cliente, vendedor, ...produtos) {
  console.log(`Venda: ${cliente} com ${vendedor}`);
  produtos.forEach(p => console.log(`- ${p}`));
}
```

## 4. Destructuring Avançado

### O que é?
Destructuring permite extrair valores de objetos e arrays de forma elegante, com suporte a:
- Renomeação de variáveis
- Valores padrão
- Destructuring aninhado

### Exemplos Práticos

#### Destructuring de Objetos
```javascript
const pedido = {
  id: '123',
  cliente: {
    nome: 'Ana Silva',
    contato: {
      email: 'ana@email.com',
      telefone: '11999999999'
    }
  },
  produtos: [
    { nome: 'Notebook', preco: 3500 },
    { nome: 'Mouse', preco: 120 }
  ]
};

// Destructuring aninhado com renomeação
const {
  id: numeroPedido,
  cliente: {
    nome: nomeCliente,
    contato: { email, telefone }
  }
} = pedido;
```

#### Em Parâmetros de Função
```javascript
function processarPedido({
  id,
  cliente: { nome },
  produtos = [],
  status = 'novo'
} = {}) {
  console.log(`Processando pedido ${id} para ${nome}`);
}
```

#### Com Arrays
```javascript
const [primeiro, segundo, ...resto] = [1, 2, 3, 4, 5];
console.log(primeiro); // 1
console.log(resto);    // [3, 4, 5]
```

## 5. Null Coalescing

### O que é?
O operador de coalescência nula (??) é uma feature moderna que permite verificar valores null ou undefined de forma mais elegante.

### Por que usar?
- ✅ Código mais limpo e seguro
- ✅ Evita erros comuns com valores falsy
- ✅ Melhor que OR (||) para alguns casos
- ✅ Mais preciso para verificações de nulidade

### Sintaxe e Exemplos

#### Básico
```javascript
const valor1 = null ?? "valor padrão";  // "valor padrão"
const valor2 = 0 ?? "valor padrão";     // 0
const valor3 = "" ?? "valor padrão";    // ""
const valor4 = undefined ?? "valor padrão"; // "valor padrão"
```

#### Comparação com OR (||)
```javascript
// O operador || considera todos os valores falsy
console.log(0 || "valor padrão");      // "valor padrão"
console.log(0 ?? "valor padrão");      // 0

console.log("" || "valor padrão");     // "valor padrão"
console.log("" ?? "valor padrão");     // ""
```

#### Exemplo Prático: Configurações de Usuário
```javascript
const userConfig = {
  theme: null,
  fontSize: 0,
  notifications: false
};

// Com ??
const theme = userConfig.theme ?? 'light';         // 'light'
const fontSize = userConfig.fontSize ?? 16;        // 0
const notifications = userConfig.notifications ?? true; // false

// Encadeamento
const config = {
  theme: userConfig.theme ?? 'light',
  fontSize: userConfig.fontSize ?? 16,
  notifications: userConfig.notifications ?? true
};
```

#### Exemplo Real: API Response
```javascript
const getProductData = (response) => {
  const {
    name = 'Produto Sem Nome',
    price = 0,
    description = 'Sem descrição',
    stock = {
      quantity: 0,
      location: 'N/A'
    }
  } = response ?? {};

  return {
    productName: name,
    productPrice: price,
    inStock: stock.quantity ?? 0,
    warehouse: stock.location ?? 'Sem localização'
  };
};
```

### Boas Práticas
1. Use `??` quando precisar distinguir especificamente entre `null`/`undefined` e outros valores falsy
2. Combine com optional chaining (`?.`) para acessos seguros a objetos aninhados
3. Prefira `??` ao invés de `||` quando trabalhar com números e strings vazias
4. Mantenha valores padrão significativos e documentados

### Casos de Uso Comuns
- Configurações de usuário
- Valores padrão em APIs
- Fallbacks em sistemas de cache
- Inicialização segura de variáveis
