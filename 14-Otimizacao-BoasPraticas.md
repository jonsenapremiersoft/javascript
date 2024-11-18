# Otimização e Boas Práticas

## 1. Debug e Performance 🔍

### 1.1 Ferramentas de Debug

#### Console Methods
O `console` oferece muito mais que apenas `console.log()`. Aqui estão ferramentas poderosas:

```javascript
// Agrupando logs relacionados
console.group('Dados do Usuário');
console.log('Nome:', usuario.nome);
console.log('Idade:', usuario.idade);
console.groupEnd();

// Medindo tempo de execução
console.time('Operação');
operacaoCompleta();
console.timeEnd('Operação');

// Criando tabelas para dados estruturados
const usuarios = [
  { nome: 'Ana', idade: 25 },
  { nome: 'João', idade: 30 }
];
console.table(usuarios);
```

#### Chrome DevTools
- **Performance Tab**: Analise o desempenho da sua aplicação
- **Network Tab**: Monitore requisições de rede
- **Memory Tab**: Identifique vazamentos de memória

### 1.2 Técnicas de Performance

#### 1.2.1 Debounce
Útil para eventos que acontecem frequentemente, como pesquisa em tempo real:

```javascript
function debounce(func, wait) {
  let timeout;
  
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };

    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

// Exemplo prático: Pesquisa em tempo real
const searchInput = document.querySelector('#search');
const handleSearch = debounce((event) => {
  // Realizar pesquisa
  searchApi(event.target.value);
}, 500);

searchInput.addEventListener('input', handleSearch);
```

#### 1.2.2 Throttle
Limita a frequência de execução de uma função:

```javascript
function throttle(func, limit) {
  let inThrottle;
  
  return function(...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  }
}

// Exemplo: Scroll infinito otimizado
window.addEventListener('scroll', throttle(() => {
  checkForNewContent();
}, 1000));
```

## 2. Clean Code 📝

### 2.1 Nomenclatura

```javascript
// ❌ Ruim
const d = new Date();
const x = user.name;

// ✅ Bom
const currentDate = new Date();
const userName = user.name;

// ❌ Ruim
function calc(a, b) { return a + b; }

// ✅ Bom
function calculateTotalPrice(basePrice, taxAmount) {
  return basePrice + taxAmount;
}
```

### 2.2 Funções

```javascript
// ❌ Ruim: Função fazendo muitas coisas
function processUser(user) {
  validateUser(user);
  updateDatabase(user);
  sendEmail(user);
  updateUI(user);
}

// ✅ Bom: Funções pequenas e específicas
async function processUserRegistration(user) {
  await validateUserData(user);
  await saveUserToDatabase(user);
  await sendWelcomeEmail(user);
  
  return user;
}
```

### 2.3 Princípio da Responsabilidade Única

```javascript
// ❌ Ruim: Classe com múltiplas responsabilidades
class UserManager {
  constructor(user) {
    this.user = user;
  }

  saveUser() { /* ... */ }
  validateUser() { /* ... */ }
  sendEmail() { /* ... */ }
  updateUI() { /* ... */ }
}

// ✅ Bom: Classes separadas por responsabilidade
class UserValidator {
  static validate(user) { /* ... */ }
}

class UserRepository {
  static save(user) { /* ... */ }
}

class UserNotifier {
  static sendWelcomeEmail(user) { /* ... */ }
}
```

## 3. Error Handling 🚨

### 3.1 Try-Catch Estruturado

```javascript
async function fetchUserData(userId) {
  try {
    const response = await api.get(`/users/${userId}`);
    return response.data;
  } catch (error) {
    if (error.response?.status === 404) {
      throw new CustomError('USER_NOT_FOUND', 'Usuário não encontrado');
    }
    if (error.response?.status === 401) {
      throw new CustomError('UNAUTHORIZED', 'Acesso não autorizado');
    }
    throw new CustomError('UNKNOWN_ERROR', 'Erro desconhecido ao buscar usuário');
  }
}

// Classe personalizada de erro
class CustomError extends Error {
  constructor(code, message) {
    super(message);
    this.code = code;
    this.name = 'CustomError';
  }
}
```

### 3.2 Error Boundaries (React)

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    logErrorToService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Algo deu errado. Por favor, tente novamente.</h1>;
    }

    return this.props.children;
  }
}
```

## 4. Memory Leaks 🧹

### 4.1 Causas Comuns e Soluções

#### 4.1.1 Event Listeners não removidos

```javascript
// ❌ Ruim: Event listener não removido
class Component {
  constructor() {
    this.handleClick = this.handleClick.bind(this);
    window.addEventListener('click', this.handleClick);
  }

  handleClick() {
    console.log('clicked');
  }
}

// ✅ Bom: Limpeza apropriada
class Component {
  constructor() {
    this.handleClick = this.handleClick.bind(this);
    window.addEventListener('click', this.handleClick);
  }

  handleClick() {
    console.log('clicked');
  }

  destroy() {
    window.removeEventListener('click', this.handleClick);
  }
}
```

#### 4.1.2 Closures Retendo Referências

```javascript
// ❌ Ruim: Closure retendo referência
function createHeavyObject() {
  const heavyObject = new HeavyObject();
  
  return function() {
    console.log(heavyObject);
  }
}

// ✅ Bom: Limpeza de referências
function createHeavyObject() {
  let heavyObject = new HeavyObject();
  
  const result = function() {
    console.log(heavyObject);
  }
  
  heavyObject = null; // Permite que o GC limpe o objeto
  return result;
}
```

#### 4.1.3 SetInterval não limpo

```javascript
// ❌ Ruim: SetInterval continua rodando
function startTimer() {
  setInterval(() => {
    console.log('tick');
  }, 1000);
}

// ✅ Bom: SetInterval com limpeza
function startTimer() {
  const timerId = setInterval(() => {
    console.log('tick');
  }, 1000);
  
  return () => clearInterval(timerId);
}

// Uso
const stopTimer = startTimer();
// Quando não precisar mais do timer
stopTimer();
```

### 4.2 Boas Práticas para Prevenção

1. **Use WeakMap/WeakSet** para referências que podem ser garbage collected
2. **Implemente métodos de cleanup** em componentes
3. **Monitore o uso de memória** usando Chrome DevTools
4. **Utilize ferramentas de profiling** para identificar vazamentos
5. **Documente padrões de cleanup** no projeto

```javascript
// Exemplo de uso de WeakMap
const cache = new WeakMap();

function processUser(user) {
  if (cache.has(user)) {
    return cache.get(user);
  }
  
  const result = expensiveOperation(user);
  cache.set(user, result);
  return result;
}
```

### Conclusão

A otimização e manutenção de código JavaScript requer atenção constante a vários aspectos:
- Debug eficiente usando as ferramentas certas
- Código limpo e bem estruturado
- Tratamento adequado de erros
- Prevenção de memory leaks

Lembre-se: 
- Teste seu código regularmente
- Monitore o desempenho
- Documente decisões importantes
- Mantenha-se atualizado com as melhores práticas
- Use ferramentas de análise de código (ESLint, SonarQube, etc.)
