# Frameworks e Bibliotecas JavaScript

## O que são?

- **Bibliotecas**: Coleções de funções/componentes reutilizáveis para tarefas específicas
- **Frameworks**: Estruturas completas que definem a arquitetura da aplicação

## Principais Conceitos

### 1. Componentização
- Divide interface em componentes reutilizáveis
- Facilita manutenção e teste
- Exemplo React:
```jsx
function Button({ text, onClick }) {
  return <button onClick={onClick}>{text}</button>;
}
```

### 2. Estado e Gerenciamento
```javascript
// Redux exemplo
const initialState = { count: 0 };
const reducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    default:
      return state;
  }
};
```

### 3. Virtual DOM
- Cópia da DOM em memória
- Otimiza atualizações de interface
- Usado por React, Vue.js

### 4. Roteamento
```javascript
// React Router exemplo
<Router>
  <Route path="/home" component={Home} />
  <Route path="/about" component={About} />
</Router>
```

## Principais Frameworks/Bibliotecas

1. **React**
   - Biblioteca para interfaces
   - Mantido pelo Facebook
   - Ecossistema rico

2. **Angular**
   - Framework completo
   - TypeScript por padrão
   - Mantido pelo Google

3. **Vue.js**
   - Framework progressivo
   - Curva de aprendizado suave
   - Combina conceitos do React e Angular

## Vantagens
- Desenvolvimento mais rápido
- Código padronizado
- Manutenção facilitada
- Comunidade ativa
- Soluções testadas

## Considerações
- Escolha baseada no projeto
- Avalie tamanho da comunidade
- Considere curva de aprendizado
- Verifique documentação
