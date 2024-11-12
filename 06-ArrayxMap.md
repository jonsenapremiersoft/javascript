# Quando Usar Array vs Map em JavaScript: Um Guia Prático

## Arrays: Casos de Uso

Arrays são ideais quando você precisa de:

### 1. Listas Ordenadas
Arrays mantêm a ordem dos elementos e são perfeitos quando a ordem importa.

```javascript
// ✅ Bom uso de Array: Lista de tarefas ordenadas por prioridade
const tarefas = [
    { id: 1, descricao: 'Urgente: Resolver bug crítico', prioridade: 1 },
    { id: 2, descricao: 'Importante: Atualizar documentação', prioridade: 2 },
    { id: 3, descricao: 'Normal: Revisar código', prioridade: 3 }
];
```

### 2. Coleções de Dados do Mesmo Tipo
Quando você tem múltiplos itens do mesmo tipo que precisam ser processados juntos.

```javascript
// ✅ Bom uso de Array: Lista de produtos em um catálogo
const produtos = [
    { id: 1, nome: 'Notebook', preco: 3000 },
    { id: 2, nome: 'Smartphone', preco: 1500 },
    { id: 3, nome: 'Tablet', preco: 800 }
];

// Fácil de processar com métodos de array
const produtosComDesconto = produtos.map(produto => ({
    ...produto,
    precoComDesconto: produto.preco * 0.9
}));
```

### 3. Operações em Lote
Quando você precisa realizar operações em múltiplos elementos.

```javascript
// ✅ Bom uso de Array: Processamento de notas de alunos
const notas = [7.5, 8.0, 6.5, 9.0, 7.0];

const media = notas.reduce((sum, nota) => sum + nota, 0) / notas.length;
const aprovados = notas.filter(nota => nota >= 7.0);
```

### 4. Dados que Precisam ser Iterados Sequencialmente
Quando você precisa percorrer elementos em ordem.

```javascript
// ✅ Bom uso de Array: Passos de um tutorial
const tutorialSteps = [
    'Criar conta',
    'Confirmar email',
    'Completar perfil',
    'Começar a usar'
];

tutorialSteps.forEach((step, index) => {
    console.log(`Passo ${index + 1}: ${step}`);
});
```

## Map: Casos de Uso

Maps são ideais quando você precisa de:

### 1. Pares Chave-Valor com Chaves de Qualquer Tipo
Quando você precisa usar objetos, números ou até mesmo outros arrays como chaves.

```javascript
// ✅ Bom uso de Map: Cache de objetos usando outros objetos como chave
const userCache = new Map();
const userObject = { id: 1, name: 'João' };

userCache.set(userObject, { lastAccess: new Date(), data: 'Dados em cache' });
```

### 2. Frequente Adição/Remoção de Pares Chave-Valor
Maps têm melhor performance para operações de adição e remoção frequentes.

```javascript
// ✅ Bom uso de Map: Sistema de sessões de usuários online
const sessoesAtivas = new Map();

// Adicionar sessão
sessoesAtivas.set('usuario123', {
    inicio: new Date(),
    dadosSessao: { /* ... */ }
});

// Remover sessão
sessoesAtivas.delete('usuario123');

// Verificar sessão
if (sessoesAtivas.has('usuario123')) {
    // Usuário está online
}
```

### 3. Necessidade de Verificação Frequente de Existência
Maps têm método `has()` otimizado para verificação de existência.

```javascript
// ✅ Bom uso de Map: Sistema de cache de permissões
const permissoesUsuario = new Map();

permissoesUsuario.set('user123', ['read', 'write']);

function verificarPermissao(userId, permissao) {
    if (!permissoesUsuario.has(userId)) {
        return false;
    }
    return permissoesUsuario.get(userId).includes(permissao);
}
```

### 4. Mapeamento de Valores que Mudam Frequentemente
Quando você precisa manter um registro atualizado de pares chave-valor.

```javascript
// ✅ Bom uso de Map: Sistema de contagem de votos em tempo real
const votacao = new Map();

function registrarVoto(candidato) {
    const votosAtuais = votacao.get(candidato) || 0;
    votacao.set(candidato, votosAtuais + 1);
}

function obterResultado(candidato) {
    return votacao.get(candidato) || 0;
}
```

## Quando NÃO Usar Cada Um

### Não Use Array Quando:

```javascript
// ❌ Mau uso de Array: Buscas frequentes por valor
const usuarios = [
    { id: 'user123', nome: 'João' },
    { id: 'user456', nome: 'Maria' }
];

// Ineficiente para buscas frequentes
const usuario = usuarios.find(u => u.id === 'user123');

// ✅ Melhor usar Map
const usuariosMap = new Map([
    ['user123', { nome: 'João' }],
    ['user456', { nome: 'Maria' }]
]);
const usuario = usuariosMap.get('user123');
```

### Não Use Map Quando:

```javascript
// ❌ Mau uso de Map: Dados que precisam ser serializados em JSON
const dadosMap = new Map([
    ['nome', 'João'],
    ['idade', 30]
]);

// Maps não são serializados corretamente em JSON
const json = JSON.stringify(dadosMap); // Resultado não é o esperado

// ✅ Melhor usar Object ou Array
const dados = {
    nome: 'João',
    idade: 30
};
const json = JSON.stringify(dados);
```

## Tabela Comparativa

| Característica | Array | Map |
|----------------|-------|-----|
| Ordem dos elementos | Mantém ordem | Mantém ordem de inserção |
| Tipo de chaves | Apenas números (índices) | Qualquer valor |
| Performance em buscas | O(n) | O(1) |
| Serialização JSON | Sim | Não |
| Iteração | Vários métodos úteis (map, filter, etc.) | Apenas forEach |
| Tamanho | length | size |
| Uso de memória | Menor | Maior |
| Melhor para | Listas ordenadas, processamento sequencial | Dicionários, caches, registros chave-valor |

## Exemplo de Decisão na Prática

Vamos ver um exemplo de como escolher entre Array e Map em um sistema real:

```javascript
// Cenário: Sistema de gerenciamento de pedidos em um restaurante

// ✅ Usar Array para a fila de pedidos (ordem importa)
const filaPedidos = [
    { numero: 1, mesa: 5, status: 'preparando' },
    { numero: 2, mesa: 3, status: 'pronto' },
    { numero: 3, mesa: 7, status: 'aguardando' }
];

// ✅ Usar Map para o status das mesas (acesso rápido por chave)
const statusMesas = new Map();
statusMesas.set(5, { ocupada: true, tempoOcupacao: '30min', pedidoAtual: 1 });
statusMesas.set(3, { ocupada: true, tempoOcupacao: '45min', pedidoAtual: 2 });
statusMesas.set(7, { ocupada: true, tempoOcupacao: '15min', pedidoAtual: 3 });

// Exemplo de uso combinado
function processarPedido(numeroPedido) {
    const pedido = filaPedidos.find(p => p.numero === numeroPedido);
    if (pedido) {
        const statusMesa = statusMesas.get(pedido.mesa);
        // Processar pedido...
    }
}
```

## Conclusão

- Use **Array** quando:
  - A ordem dos elementos é importante
  - Você precisa processar elementos sequencialmente
  - Você precisa usar métodos como map, filter, reduce
  - Os dados precisam ser serializados em JSON

- Use **Map** quando:
  - Você precisa de chaves que não são números
  - Você faz muitas operações de busca por chave
  - Você precisa adicionar/remover pares frequentemente
  - Você precisa manter um registro chave-valor atualizado

A escolha entre Array e Map pode impactar significativamente a performance e a clareza do seu código. Sempre considere os requisitos específicos do seu caso de uso antes de fazer sua escolha.
