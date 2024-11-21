# Bundlers e Importações

## Origem dos Pacotes e Módulos

JavaScript originalmente não possuía um sistema nativo de módulos. Todo código era executado no escopo global, causando conflitos de nomes e dificultando a manutenção de projetos grandes.

Para resolver isso, a comunidade desenvolveu diferentes padrões de módulos:

- CommonJS (Node.js) - Usa `require()`
- AMD (Asynchronous Module Definition) 
- UMD (Universal Module Definition)
- ESModules (Padrão atual) - Usa `import/export`

### Por que não podemos usar import/require diretamente no navegador?

1. **Segurança**: Navegadores restringem acesso direto ao sistema de arquivos
2. **Performance**: Carregar múltiplos arquivos HTTP separadamente é ineficiente
3. **Dependências**: Navegadores não resolvem automaticamente árvores de dependências
4. **Compatibilidade**: Nem todos navegadores suportam ESModules nativamente

## Principais Bundlers

### Webpack
```javascript
// webpack.config.js
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
}
```

**Características**:
- Mais popular e completo
- Suporta code splitting
- Hot Module Replacement (HMR)
- Extensível via plugins/loaders
- Otimizado para Single Page Applications

### Vite
```javascript
// vite.config.js
export default {
  root: './src',
  build: {
    outDir: '../dist'
  }
}
```

**Características**:
- Desenvolvido para modernos frameworks
- Extremamente rápido em desenvolvimento
- Usa ESModules nativos em dev
- Bundling otimizado em produção
- Menor configuração necessária

### Rollup
```javascript
// rollup.config.js
export default {
  input: 'src/main.js',
  output: {
    file: 'bundle.js',
    format: 'iife'
  }
}
```

**Características**:
- Focado em bibliotecas
- Tree-shaking superior
- Bundles mais limpos
- Configuração simples
- Ótimo para ESModules

## Sistema de Módulos

### ESModules (import/export)

#### Named Exports
```javascript
// math.js
export const sum = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// main.js
import { sum, subtract } from './math.js';
console.log(sum(5, 3));     // 8
```

#### Default Export
```javascript
// user.js
export default class User {
  constructor(name) {
    this.name = name;
  }
}

// main.js
import User from './user.js';
const user = new User('João');
```

#### Re-exporting
```javascript
// index.js
export { default as User } from './user.js';
export * from './math.js';
```

### CommonJS (require)

```javascript
// helpers.js
module.exports = {
  formatDate: (date) => {
    return date.toLocaleDateString();
  }
};

// main.js
const { formatDate } = require('./helpers.js');
console.log(formatDate(new Date()));
```

### Diferenças Importantes

1. **ESModules**:
   - Estático e analisado em tempo de compilação
   - Suporta importação assíncrona (`import()`)
   - Melhor tree-shaking
   - Mais verboso mas mais claro

2. **CommonJS**:
   - Dinâmico e resolvido em tempo de execução
   - Mais simples e direto
   - Padrão no Node.js
   - Não suporta importação assíncrona nativamente

## Melhores Práticas

1. **Use ESModules para novos projetos**
   ```javascript
   // Prefira:
   import { Component } from './component';
   
   // Ao invés de:
   const Component = require('./component');
   ```

2. **Nomeie exports claramente**
   ```javascript
   // Bom
   export const calculateTotalPrice = (items) => {...};
   
   // Evite
   export const calc = (i) => {...};
   ```

3. **Agrupe exports relacionados**
   ```javascript
   // utils/index.js
   export * from './date';
   export * from './number';
   export * from './string';
   ```

4. **Use path aliases para imports mais limpos**
   ```javascript
   // Com alias configurado no bundler
   import { Button } from '@components/Button';
   // Ao invés de
   import { Button } from '../../../components/Button';
   ```

