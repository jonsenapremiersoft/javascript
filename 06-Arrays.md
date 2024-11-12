# Arrays

## 1. Introdução aos Arrays

Um array é uma estrutura de dados que permite armazenar múltiplos valores em uma única variável. Em JavaScript, arrays são extremamente versáteis e podem conter diferentes tipos de dados.

```javascript
// Criando arrays
const frutas = ['maçã', 'banana', 'laranja'];
const misturado = [1, 'texto', true, { nome: 'João' }];
```

## 2. Métodos Principais de Array

### 2.1 forEach
O forEach é usado para executar uma função para cada elemento do array, sem criar um novo array.

```javascript
// Exemplo prático: Enviando notificações para uma lista de usuários
const usuarios = [
    { nome: 'Maria', email: 'maria@email.com' },
    { nome: 'João', email: 'joao@email.com' },
    { nome: 'Ana', email: 'ana@email.com' }
];

usuarios.forEach(usuario => {
    console.log(`Enviando email para ${usuario.nome} no endereço ${usuario.email}`);
});
```

### 2.2 map
O map cria um novo array com os resultados de uma função aplicada a cada elemento.

```javascript
// Exemplo prático: Calculando preços com desconto
const produtos = [
    { nome: 'Notebook', preco: 3000 },
    { nome: 'Smartphone', preco: 1500 },
    { nome: 'Tablet', preco: 800 }
];

const produtosComDesconto = produtos.map(produto => ({
    ...produto,
    precoComDesconto: produto.preco * 0.9 // 10% de desconto
}));
```

### 2.3 filter
O filter cria um novo array com todos os elementos que passam em um teste.

```javascript
// Exemplo prático: Filtrando produtos em estoque
const produtosLoja = [
    { nome: 'Notebook', emEstoque: true, preco: 3000 },
    { nome: 'Smartphone', emEstoque: false, preco: 1500 },
    { nome: 'Tablet', emEstoque: true, preco: 800 }
];

const produtosDisponiveis = produtosLoja.filter(produto => produto.emEstoque);
```

### 2.4 reduce
O reduce executa uma função redutora em cada elemento do array, resultando em um único valor.

```javascript
// Exemplo prático: Calculando valor total de vendas
const vendas = [
    { produto: 'Notebook', valor: 3000 },
    { produto: 'Mouse', valor: 80 },
    { produto: 'Teclado', valor: 150 }
];

const totalVendas = vendas.reduce((total, venda) => total + venda.valor, 0);
```

## 3. Ordenação e Busca

### 3.1 sort
O sort ordena os elementos de um array.

```javascript
// Exemplo prático: Ordenando produtos por preço
const produtosOrdenados = produtos.sort((a, b) => a.preco - b.preco);

// Ordenando strings (case-sensitive)
const nomes = ['João', 'Maria', 'Ana', 'Carlos'];
nomes.sort();
```

### 3.2 find e findIndex
O find retorna o primeiro elemento que satisfaz uma condição, enquanto findIndex retorna sua posição.

```javascript
// Exemplo prático: Buscando um usuário
const usuarios = [
    { id: 1, nome: 'Maria' },
    { id: 2, nome: 'João' },
    { id: 3, nome: 'Ana' }
];

const usuario = usuarios.find(user => user.id === 2);
const posicaoUsuario = usuarios.findIndex(user => user.id === 2);
```


## 4. Spread Operator (...)

O Spread Operator é um recurso poderoso que permite "espalhar" elementos de um array ou objeto. É representado por três pontos (...) e tem diversos casos de uso úteis.

### 4.1 Copiando Arrays

```javascript
// Fazendo uma cópia superficial de um array
const frutas = ['maçã', 'banana', 'laranja'];
const frutasCopia = [...frutas];

// A cópia é independente do original
frutas.push('manga');
console.log(frutas);       // ['maçã', 'banana', 'laranja', 'manga']
console.log(frutasCopia);  // ['maçã', 'banana', 'laranja']
```

### 4.2 Combinando Arrays

```javascript
// Unindo arrays
const frutasVermelhas = ['morango', 'cereja'];
const frutrasCitricas = ['laranja', 'limão'];
const todasFrutas = [...frutasVermelhas, ...frutrasCitricas];

// Adicionando elementos ao combinar
const maisFrutas = [...frutasVermelhas, 'maçã', ...frutrasCitricas];
```

### 4.3 Passando Arrays como Argumentos

```javascript
// Usando spread para passar múltiplos argumentos
const numeros = [1, 5, 2, 8, 3];

// Sem spread operator
console.log(Math.max(1, 5, 2, 8, 3));

// Com spread operator
console.log(Math.max(...numeros));

// Exemplo prático: Função de registro de vendas
function registrarVenda(data, vendedor, ...produtos) {
    console.log(`Venda realizada em ${data} por ${vendedor}`);
    produtos.forEach(produto => console.log(`- ${produto}`));
}

registrarVenda('2024-03-15', 'João', 'Notebook', 'Mouse', 'Teclado');
```

### 4.4 Casos de Uso Práticos

#### Exemplo 1: Sistema de Carrinho de Compras
```javascript
const carrinhoAtual = [
    { id: 1, nome: 'Produto A', preco: 50 },
    { id: 2, nome: 'Produto B', preco: 30 }
];

// Adicionando novo produto mantendo imutabilidade
const novoProduto = { id: 3, nome: 'Produto C', preco: 40 };
const carrinhoAtualizado = [...carrinhoAtual, novoProduto];

// Removendo um produto de forma imutável
const carrinhoSemProdutoB = carrinhoAtual.filter(produto => produto.id !== 2);
const carrinhoFinal = [...carrinhoSemProdutoB];
```

#### Exemplo 2: Gerenciamento de Estado
```javascript
const estadoInicial = {
    usuarios: ['João', 'Maria'],
    configuracoes: { tema: 'claro' }
};

// Atualizando estado de forma imutável
const novoEstado = {
    ...estadoInicial,
    usuarios: [...estadoInicial.usuarios, 'Pedro']
};
```

#### Exemplo 3: Mesclando Configurações
```javascript
const configPadrao = {
    tema: 'claro',
    idioma: 'pt-BR',
    notifications: true
};

const configUsuario = {
    tema: 'escuro',
    tamanhoFonte: 'grande'
};

// Mesclando configurações, com preferência para configUsuario
const configFinal = {
    ...configPadrao,
    ...configUsuario
};
```

#### Exemplo 4: Manipulação de Formulários
```javascript
const dadosFormulario = {
    nome: 'João',
    email: 'joao@email.com'
};

// Atualizando apenas um campo
const formAtualizado = {
    ...dadosFormulario,
    email: 'novo@email.com'
};
```

### 4.5 Boas Práticas com Spread Operator

1. **Imutabilidade**
```javascript
// ❌ Evite modificar arrays diretamente
const array = [1, 2, 3];
array.push(4);

// ✅ Use spread para manter imutabilidade
const array = [1, 2, 3];
const novoArray = [...array, 4];
```

2. **Cópias Superficiais vs. Profundas**
```javascript
// ⚠️ Cuidado com objetos aninhados
const usuario = {
    nome: 'João',
    endereco: { cidade: 'São Paulo' }
};

const usuarioCopia = { ...usuario };
usuarioCopia.endereco.cidade = 'Rio'; // Modifica o objeto original também!

// ✅ Para cópia profunda, considere:
const usuarioCopiaCompleta = JSON.parse(JSON.stringify(usuario));
// Ou use bibliotecas como lodash cloneDeep
```

3. **Performance**
```javascript
// ⚠️ Evite spread excessivo em loops
const arrays = [[1, 2], [3, 4], [5, 6]];

// ❌ Pode ser custoso com arrays grandes
arrays.reduce((acc, curr) => [...acc, ...curr], []);

// ✅ Melhor usar concat ou flat
arrays.reduce((acc, curr) => acc.concat(curr), []);
// ou
arrays.flat();
```

### 4.6 Exercícios com Spread Operator

1. **Exercício: Gerenciador de Tarefas**
```javascript
const tarefasIniciais = [
    { id: 1, texto: 'Estudar JavaScript', concluida: false },
    { id: 2, texto: 'Fazer exercícios', concluida: false }
];

// Tarefas:
// 1. Adicione uma nova tarefa sem modificar o array original
// 2. Marque uma tarefa como concluída mantendo imutabilidade
// 3. Combine duas listas de tarefas diferentes
// 4. Remova uma tarefa específica mantendo imutabilidade
```

2. **Exercício: Sistema de Reservas**
```javascript
const reservasAtuais = [
    { id: 1, sala: 'A1', horario: '09:00' },
    { id: 2, sala: 'B1', horario: '10:00' }
];

// Tarefas:
// 1. Adicione uma nova reserva
// 2. Atualize o horário de uma reserva existente
// 3. Combine reservas de duas salas diferentes
// 4. Crie uma função que aceite múltiplas reservas como argumentos
```

## 4.7 Notas Finais

O Spread Operator é uma ferramenta poderosa que:
- Facilita a manipulação de arrays e objetos de forma imutável
- Torna o código mais limpo e legível
- É essencial para programação funcional em JavaScript
- Deve ser usado com consciência em relação à performance

Lembre-se sempre de considerar:
- A necessidade de cópias profundas vs. superficiais
- O impacto na performance ao trabalhar com grandes conjuntos de dados
- A legibilidade do código ao combinar múltiplos spreads

## 5. Objeto Map

O Map é uma estrutura de dados que permite armazenar pares de chave-valor, onde as chaves podem ser de qualquer tipo.

```javascript
// Exemplo prático: Registro de votos
const votacao = new Map();

// Registrando votos
votacao.set('Candidato A', 150);
votacao.set('Candidato B', 120);

// Obtendo resultado
console.log(votacao.get('Candidato A')); // 150

// Verificando se existe
console.log(votacao.has('Candidato C')); // false

// Removendo entrada
votacao.delete('Candidato B');
```

## 6. Boas Práticas

1. Sempre prefira métodos imutáveis (map, filter, reduce) em vez de modificar o array original
2. Use nomes descritivos para suas variáveis e funções
3. Aproveite arrow functions para código mais conciso
4. Utilize destructuring quando possível
5. Considere o uso de métodos encadeados para operações complexas

```javascript
// Exemplo de boas práticas combinadas
const vendas = [
    { produto: 'Notebook', valor: 3000, categoria: 'Eletrônicos' },
    { produto: 'Mouse', valor: 80, categoria: 'Acessórios' },
    { produto: 'Teclado', valor: 150, categoria: 'Acessórios' }
];

const totalAcessorios = vendas
    .filter(({ categoria }) => categoria === 'Acessórios')
    .map(({ valor }) => valor)
    .reduce((total, valor) => total + valor, 0);
```

## 7. Exercícios Práticos

### Exercício 1: Sistema de Biblioteca
Crie um sistema que gerencie livros em uma biblioteca:

```javascript
const livros = [
    { id: 1, titulo: 'JavaScript Avançado', emprestado: false },
    { id: 2, titulo: 'Python Básico', emprestado: true },
    { id: 3, titulo: 'Node.js na Prática', emprestado: false }
];

// Tarefas:
// 1. Liste todos os livros disponíveis (não emprestados)
// 2. Adicione um novo livro à biblioteca
// 3. Marque um livro como emprestado
// 4. Calcule quantos livros estão emprestados
```

### Exercício 2: Gestão de Estudantes
Trabalhe com uma lista de estudantes e suas notas:

```javascript
const estudantes = [
    { nome: 'Ana', notas: [8, 7, 9] },
    { nome: 'Pedro', notas: [6, 8, 7] },
    { nome: 'Maria', notas: [9, 9, 8] }
];

// Tarefas:
// 1. Calcule a média de cada estudante
// 2. Encontre o estudante com a maior média
// 3. Liste apenas os estudantes aprovados (média >= 7)
// 4. Adicione uma nova nota para cada estudante
```

### Exercício 3: E-commerce
Trabalhe com um carrinho de compras:

```javascript
const carrinho = [
    { id: 1, produto: 'Smartphone', preco: 1500, quantidade: 2 },
    { id: 2, produto: 'Notebook', preco: 3000, quantidade: 1 },
    { id: 3, produto: 'Mouse', preco: 80, quantidade: 3 }
];

// Tarefas:
// 1. Calcule o valor total do carrinho
// 2. Aplique um desconto de 10% em todos os produtos
// 3. Remova produtos com quantidade zero
// 4. Encontre o produto mais caro do carrinho
```

### Exercício 4: Análise de Dados
Trabalhe com dados de uma empresa:

```javascript
const funcionarios = [
    { nome: 'João', departamento: 'TI', salario: 5000 },
    { nome: 'Maria', departamento: 'RH', salario: 4000 },
    { nome: 'Pedro', departamento: 'TI', salario: 6000 }
];

// Tarefas:
// 1. Calcule a média salarial por departamento
// 2. Encontre o funcionário com maior salário
// 3. Liste os funcionários em ordem alfabética
// 4. Agrupe os funcionários por departamento usando Map
```

Para cada exercício, tente resolver primeiro sozinho. Se precisar de ajuda, aqui estão algumas dicas:
- Use os métodos apropriados para cada situação
- Quebre o problema em partes menores
- Teste sua solução com diferentes cenários
- Verifique se sua solução segue as boas práticas

Boa prática! 🚀
