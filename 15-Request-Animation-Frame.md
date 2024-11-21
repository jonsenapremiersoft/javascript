# Como funciona o requestAnimationFrame?

O método `requestAnimationFrame` é uma função em JavaScript utilizada para realizar animações eficientes no navegador. Ele informa ao navegador que você deseja realizar uma animação e solicita que este agende a atualização da próxima tela para o melhor momento.

## Principais características

1. **Eficiência**: O `requestAnimationFrame` sincroniza a taxa de atualização da animação com a taxa de atualização do monitor (normalmente 60 fps), garantindo animações mais suaves e menos uso de recursos do que `setInterval` ou `setTimeout`.

2. **Pausa em abas inativas**: Quando a aba do navegador não está visível, o navegador pausa as execuções agendadas por `requestAnimationFrame`, economizando recursos e evitando processamento desnecessário.

3. **Função Recursiva**: Para criar animações contínuas, você chama o `requestAnimationFrame` dentro da própria função de callback.

---

## Como usar o `requestAnimationFrame`?

Um exemplo básico de animação de um quadrado que se move horizontalmente:

```javascript
let position = 0;
const speed = 2; // Pixels por frame
const square = document.getElementById('square'); // Elemento HTML

function animate() {
    position += speed; // Atualiza a posição
    square.style.transform = `translateX(${position}px)`; // Move o quadrado

    if (position < window.innerWidth - square.offsetWidth) {
        requestAnimationFrame(animate); // Chama novamente para continuar
    }
}

animate(); // Inicia a animação
```

## Funcionamento Passo a Passo

- Define o estado inicial: Configura variáveis, como posição inicial e velocidade.
- Função de animação: Define o que acontece a cada quadro, como atualizar a posição ou redimensionar elementos.
- Recursão: Dentro da função de animação, chama requestAnimationFrame novamente para continuar a execução na próxima atualização.


## Diferença: requestAnimationFrame x setInterval

- Taxa de atualização:	Sincronizado com o monitor (normalmente 60fps) x Independente (fixa)
- Eficiência:	Pausa em abas inativas x Continua executando
- Suavidade:	Alta (evita tearing ou jittering) x	Menor (descompasso com FPS)
- Uso de recursos:	Menor (otimizado pelo navegador) x Maior (processa desnecessariamente)
