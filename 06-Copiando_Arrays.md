Copiando Arrays em JavaScript
## Shallow Copy vs Deep Copy

#### O que é uma cópia de array?
Em JavaScript, frequentemente precisamos criar cópias de arrays para trabalhar com os dados sem modificar o array original. É como fazer uma fotocópia de um documento: você quer uma nova versão para fazer anotações sem estragar o original.

### 🔍 Os Dois Tipos de Cópia

#### 1. Cópia Rasa (Shallow Copy)
Imagine que você tem uma caixa (array) com fotos (objetos). Quando você faz uma cópia rasa:
- Você cria uma nova caixa
- Mas coloca as MESMAS fotos dentro dela
- Se você riscar uma foto, ela ficará riscada em AMBAS as caixas!

```javascript
// Exemplo de Cópia Rasa
const minhasTarefas = [
    { id: 1, texto: "Estudar", concluida: false }
];

const copiaTarefas = [...minhasTarefas];
copiaTarefas[0].concluida = true;

console.log(minhasTarefas[0].concluida);  // true 😱
// A tarefa original também foi marcada como concluída!
```

#### 2. Cópia Profunda (Deep Copy)
Agora imagine que, em vez de mover as mesmas fotos, você:
- Cria uma nova caixa
- Faz CÓPIAS de cada foto
- Coloca as cópias na nova caixa
- Agora você pode riscar uma foto sem afetar a outra!

```javascript
// Exemplo de Cópia Profunda
const minhasTarefas = [
    { id: 1, texto: "Estudar", concluida: false }
];

const copiaTarefas = minhasTarefas.map(tarefa => ({...tarefa}));
copiaTarefas[0].concluida = true;

console.log(minhasTarefas[0].concluida);  // false 😌
// A tarefa original permanece intacta!
```

### 🛠️ Como Fazer na Prática

#### Formas de fazer uma Cópia Profunda:

1. Usando map com spread operator (Recomendado para arrays simples):
```javascript
const copiaSegura = arrayOriginal.map(item => ({...item}));
```

2. Usando JSON (Para casos mais simples):
```javascript
const copiaSegura = JSON.parse(JSON.stringify(arrayOriginal));
```

3. Usando o método moderno structuredClone (Mais recente):
```javascript
const copiaSegura = structuredClone(arrayOriginal);
```
