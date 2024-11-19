# Delays, Sleep, Pause & Wait

## 1. Introdução
Em JavaScript, existem várias maneiras de implementar delays, pausas e esperas em nosso código. Cada método tem seus casos de uso específicos e particularidades.

## 2. setTimeout
O método mais básico para criar delays em JavaScript.

```javascript
// Sintaxe básica
setTimeout(() => {
    console.log("Executado após 2 segundos");
}, 2000);

// Exemplo prático
function alertaComDelay() {
    console.log("Início");
    setTimeout(() => {
        console.log("Passaram-se 3 segundos");
    }, 3000);
    console.log("Fim");
}

// O código acima imprimirá:
// "Início"
// "Fim"
// (após 3 segundos) "Passaram-se 3 segundos"
```

## 3. setInterval
Para execuções repetidas com intervalo fixo.

```javascript
// Sintaxe básica
const intervalId = setInterval(() => {
    console.log("Executado a cada 1 segundo");
}, 1000);

// Para parar o intervalo
clearInterval(intervalId);

// Exemplo prático: contador
let contador = 0;
const intervalo = setInterval(() => {
    contador++;
    console.log(contador);
    if (contador >= 5) {
        clearInterval(intervalo);
    }
}, 1000);
```

## 4. Promise e async/await
Método moderno para criar delays de forma mais elegante.

```javascript
// Função sleep usando Promise
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

// Usando com async/await
async function exemplo() {
    console.log("Início");
    await sleep(2000);
    console.log("Após 2 segundos");
    await sleep(1000);
    console.log("Após mais 1 segundo");
}

// Exemplo prático: carregamento simulado
async function simularCarregamento() {
    console.log("Carregando...");
    await sleep(2000);
    console.log("25%");
    await sleep(1000);
    console.log("50%");
    await sleep(1000);
    console.log("75%");
    await sleep(1000);
    console.log("100% - Concluído!");
}
```

## 5. requestAnimationFrame
Para animações suaves e otimizadas.

```javascript
function animarComRAF() {
    let start = null;
    const duration = 2000; // 2 segundos

    function animate(timestamp) {
        if (!start) start = timestamp;
        const progress = timestamp - start;

        // Fazer algo com o progresso
        console.log(`Progresso: ${Math.min(progress / duration * 100, 100)}%`);

        if (progress < duration) {
            requestAnimationFrame(animate);
        }
    }

    requestAnimationFrame(animate);
}
```

## 6. Casos de Uso Práticos

### 6.1. Debounce (aguardar input do usuário)
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

// Exemplo de uso
const processarInput = debounce(() => {
    console.log("Processando input...");
}, 500);

// Em um evento de input
// inputElement.addEventListener('input', processarInput);
```

### 6.2. Throttle (limitar frequência de execução)
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

// Exemplo de uso
const handleScroll = throttle(() => {
    console.log("Evento de scroll processado");
}, 1000);

// window.addEventListener('scroll', handleScroll);
```

a. A função `throttle` é um controlador de frequência que limita quantas vezes uma função pode ser executada em um determinado período.

b. Parâmetros:
- `func`: A função que queremos controlar
- `limit`: Tempo mínimo (em ms) entre execuções

c. Funcionamento interno:
```javascript
let inThrottle; // Flag que controla se estamos no período de espera

return function(...args) { // Função wrapper que será retornada
    if (!inThrottle) { // Só executa se não estiver no período de espera
        func.apply(this, args); // Executa a função original
        inThrottle = true; // Ativa o período de espera
        setTimeout(() => inThrottle = false, limit); // Agenda a liberação
    }
}
```

5. No exemplo de uso:
```javascript
const handleScroll = throttle(() => {
    console.log("Evento de scroll processado");
}, 1000);
```
- Se o usuário rolar a página 100 vezes em 1 segundo
- O log só será exibido 1 vez
- Novas chamadas durante o período de 1000ms são ignoradas
- Após 1000ms, a função pode ser executada novamente

Este padrão é útil para otimizar eventos frequentes como scroll, resize ou requisições à API.

A principal diferença entre throttle e debounce:

- Throttle:

Garante que uma função seja executada no máximo uma vez a cada X milissegundos.
Útil quando você precisa garantir uma taxa máxima de execução.
Exemplo: limitar chamadas de API durante scroll.

- Debounce:

Só executa a função depois que o usuário para de chamar ela por X milissegundos.
Agrupa várias chamadas em uma única execução.
Exemplo: busca em tempo real enquanto usuário digita.

## 7. Dicas e Boas Práticas

1. **Sempre limpe timeouts e intervalos:**
```javascript
const timeout = setTimeout(() => {}, 1000);
clearTimeout(timeout);

const interval = setInterval(() => {}, 1000);
clearInterval(interval);
```

2. **Use Promise para operações assíncronas:**
```javascript
async function operacaoComTimeout() {
    try {
        await Promise.race([
            fetch('https://api.exemplo.com/dados'),
            sleep(5000)
        ]);
    } catch (error) {
        console.log('Timeout ou erro na requisição');
    }
}
```

3. **Evite delays muito longos:**
```javascript
// Ruim
setTimeout(() => {}, 300000); // 5 minutos

// Melhor: dividir em partes menores ou usar outra abordagem
```

## 8. Exemplo prático

1. Crie um contador regressivo de 10 a 0
2. Implemente um sistema de loading com percentual
3. Crie uma função que simule um semáforo
4. Implemente um debounce para um campo de busca

### Exemplo de Solução - Semáforo:
```javascript
async function semaforo() {
    while (true) {
        console.log("🔴 Vermelho");
        await sleep(3000);
        console.log("🟡 Amarelo");
        await sleep(1000);
        console.log("🟢 Verde");
        await sleep(2000);
    }
}
```

## 9. Conclusão

Delays e pausas são fundamentais em JavaScript para:
- Controle de timing em animações
- Simulação de carregamento
- Otimização de performance
- Controle de fluxo assíncrono
- Melhor experiência do usuário

Escolha o método mais apropriado baseado no seu caso de uso específico e sempre considere a experiência do usuário ao implementar delays em sua aplicação.
