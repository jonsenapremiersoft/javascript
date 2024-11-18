# Optional Chaining

O optional chaining (`?.`) permite acessar propriedades aninhadas de objetos de forma segura, evitando erros quando alguma propriedade intermediária é `null` ou `undefined`.

## Sintaxe Básica
```javascript
objeto?.propriedade
objeto?.metodo?.()
array?.[indice]
```

## Exemplos Práticos

### 1. Dados de Usuário
```javascript
// Sem optional chaining
const getNome = usuario => {
  if (usuario && usuario.perfil && usuario.perfil.nome) {
    return usuario.perfil.nome;
  }
  return 'Nome não disponível';
}

// Com optional chaining
const getNome = usuario => usuario?.perfil?.nome ?? 'Nome não disponível';

// Uso
const usuario = {
  perfil: {
    nome: 'João'
  }
};
const usuarioIncompleto = {};

console.log(getNome(usuario)); // 'João'
console.log(getNome(usuarioIncompleto)); // 'Nome não disponível'
```

### 2. API Response
```javascript
// Dados de uma API de e-commerce
const pedido = {
  items: [
    { produto: { nome: 'Notebook' } }
  ]
};

// Acessando item seguramente
const nomePrimeiroProduto = pedido?.items?.[0]?.produto?.nome;
```

### 3. Chamada de Métodos
```javascript
// Event handlers
const handleClick = event => {
  // Previne erro se preventDefault não existir
  event?.preventDefault?.();
}
```

### 4. Integração com localStorage
```javascript
// Leitura segura de dados do localStorage
const configs = JSON.parse(localStorage.getItem('configs'))?.tema ?? 'claro';
```

O optional chaining simplifica o código e o torna mais robusto, especialmente ao lidar com dados externos ou estruturas aninhadas.
