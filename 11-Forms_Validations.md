# Formulários e Validação

## CSS Base Compartilhado
Primeiro, crie um arquivo `styles.css` que será usado em todos os exemplos:

```css
body {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 20px auto;
    padding: 20px;
}
.form-group {
    margin-bottom: 15px;
}
label {
    display: block;
    margin-bottom: 5px;
}
input, textarea, select {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
}
button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
button:hover {
    background-color: #45a049;
}
.error {
    color: red;
    font-size: 0.9em;
    margin-top: 5px;
}
.success {
    color: green;
}
.invalid {
    border-color: red;
}
.valid {
    border-color: green;
}
```

## 1. Formulário Básico com Validação

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário Básico</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Cadastro de Usuário</h2>
    
    <form id="cadastroForm">
        <div class="form-group">
            <label for="nome">Nome:</label>
            <input type="text" id="nome" required>
            <span class="error" id="nomeErro"></span>
        </div>

        <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" required>
            <span class="error" id="emailErro"></span>
        </div>

        <div class="form-group">
            <label for="senha">Senha:</label>
            <input type="password" id="senha" required>
            <span class="error" id="senhaErro"></span>
        </div>

        <button type="submit">Cadastrar</button>
    </form>

    <script>
        const form = document.getElementById('cadastroForm');
        
        form.addEventListener('submit', (e) => {
            e.preventDefault();
            let isValid = true;
            
            // Validar nome
            const nome = document.getElementById('nome');
            const nomeErro = document.getElementById('nomeErro');
            if (nome.value.length < 3) {
                nomeErro.textContent = 'Nome deve ter pelo menos 3 caracteres';
                isValid = false;
            } else {
                nomeErro.textContent = '';
            }
            
            // Validar email
            const email = document.getElementById('email');
            const emailErro = document.getElementById('emailErro');
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(email.value)) {
                emailErro.textContent = 'Email inválido';
                isValid = false;
            } else {
                emailErro.textContent = '';
            }
            
            // Validar senha
            const senha = document.getElementById('senha');
            const senhaErro = document.getElementById('senhaErro');
            if (senha.value.length < 6) {
                senhaErro.textContent = 'Senha deve ter pelo menos 6 caracteres';
                isValid = false;
            } else {
                senhaErro.textContent = '';
            }
            
            if (isValid) {
                alert('Formulário válido!');
            }
        });
    </script>
</body>
</html>
```

## 2. Formulário com Validação em Tempo Real

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Validação em Tempo Real</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Cadastro com Validação em Tempo Real</h2>
    
    <form id="cadastroRealTime">
        <div class="form-group">
            <label for="usuario">Usuário:</label>
            <input type="text" id="usuario" required>
            <span class="error" id="usuarioErro"></span>
        </div>

        <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" id="email" required>
            <span class="error" id="emailErro"></span>
        </div>

        <div class="form-group">
            <label for="cpf">CPF:</label>
            <input type="text" id="cpf" required>
            <span class="error" id="cpfErro"></span>
        </div>

        <button type="submit" id="submitBtn" disabled>Cadastrar</button>
    </form>

    <script>
        const form = document.getElementById('cadastroRealTime');
        const usuario = document.getElementById('usuario');
        const email = document.getElementById('email');
        const cpf = document.getElementById('cpf');
        const submitBtn = document.getElementById('submitBtn');

        // Função para validar CPF
        function validarCPF(cpf) {
            cpf = cpf.replace(/[^\d]+/g,'');
            if(cpf.length !== 11 || /^(\d)\1{10}$/.test(cpf)) return false;
            
            let soma = 0;
            for (let i = 0; i < 9; i++) {
                soma += parseInt(cpf.charAt(i)) * (10 - i);
            }
            let digito1 = 11 - (soma % 11);
            if (digito1 > 9) digito1 = 0;
            
            soma = 0;
            for (let i = 0; i < 10; i++) {
                soma += parseInt(cpf.charAt(i)) * (11 - i);
            }
            let digito2 = 11 - (soma % 11);
            if (digito2 > 9) digito2 = 0;
            
            return (cpf.charAt(9) == digito1 && cpf.charAt(10) == digito2);
        }

        // Validação em tempo real
        usuario.addEventListener('input', validateFields);
        email.addEventListener('input', validateFields);
        cpf.addEventListener('input', validateFields);

        function validateFields() {
            let isValid = true;
            
            // Validar usuário
            if (usuario.value.length < 3) {
                document.getElementById('usuarioErro').textContent = 'Mínimo 3 caracteres';
                usuario.classList.add('invalid');
                isValid = false;
            } else {
                document.getElementById('usuarioErro').textContent = '';
                usuario.classList.remove('invalid');
                usuario.classList.add('valid');
            }
            
            // Validar email
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (!emailRegex.test(email.value)) {
                document.getElementById('emailErro').textContent = 'Email inválido';
                email.classList.add('invalid');
                isValid = false;
            } else {
                document.getElementById('emailErro').textContent = '';
                email.classList.remove('invalid');
                email.classList.add('valid');
            }
            
            // Validar CPF
            if (!validarCPF(cpf.value)) {
                document.getElementById('cpfErro').textContent = 'CPF inválido';
                cpf.classList.add('invalid');
                isValid = false;
            } else {
                document.getElementById('cpfErro').textContent = '';
                cpf.classList.remove('invalid');
                cpf.classList.add('valid');
            }
            
            submitBtn.disabled = !isValid;
        }

        form.addEventListener('submit', (e) => {
            e.preventDefault();
            if (!submitBtn.disabled) {
                alert('Dados válidos! Enviando...');
                // Aqui você enviaria os dados para o servidor
            }
        });
    </script>
</body>
</html>
```

## 3. Formulário com localStorage

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário com localStorage</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h2>Preferências do Usuário</h2>
    
    <form id="preferencesForm">
        <div class="form-group">
            <label for="nome">Nome:</label>
            <input type="text" id="nome" required>
        </div>

        <div class="form-group">
            <label for="tema">Tema:</label>
            <select id="tema" required>
                <option value="claro">Claro</option>
                <option value="escuro">Escuro</option>
            </select>
        </div>

        <div class="form-group">
            <label for="newsletter">
                <input type="checkbox" id="newsletter">
                Receber newsletter
            </label>
        </div>

        <button type="submit">Salvar Preferências</button>
        <button type="button" onclick="limparPreferencias()">Limpar Preferências</button>
    </form>

    <script>
        const form = document.getElementById('preferencesForm');
        
        // Carregar preferências salvas
        window.addEventListener('load', () => {
            const preferences = JSON.parse(localStorage.getItem('userPreferences'));
            if (preferences) {
                document.getElementById('nome').value = preferences.nome || '';
                document.getElementById('tema').value = preferences.tema || 'claro';
                document.getElementById('newsletter').checked = preferences.newsletter || false;
            }
        });

        // Salvar preferências
        form.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const preferences = {
                nome: document.getElementById('nome').value,
                tema: document.getElementById('tema').value,
                newsletter: document.getElementById('newsletter').checked
            };
            
            localStorage.setItem('userPreferences', JSON.stringify(preferences));
            alert('Preferências salvas!');
        });

        function limparPreferencias() {
            localStorage.removeItem('userPreferences');
            form.reset();
            alert('Preferências removidas!');
        }
    </script>
</body>
</html>
```

## 4. Exercícios Práticos

### Exercício 1: Formulário de Cadastro Completo
Crie um formulário de cadastro com os seguintes campos:
- Nome completo
- Email
- CPF
- Telefone
- Data de nascimento
- Endereço completo
- Senha e confirmação de senha

Requisitos:
1. Validação em tempo real de todos os campos
2. Máscara para CPF e telefone
3. Verificação de idade mínima (18 anos)
4. Senha forte (mínimo 8 caracteres, incluindo maiúsculas, minúsculas e números)
5. Armazenar dados no localStorage
6. Botão para limpar dados salvos

### Exercício 2: Formulário de Pedido
Crie um formulário de pedido com:
- Lista de produtos com preços
- Quantidade de cada produto
- Cálculo automático do total
- Dados de entrega
- Método de pagamento

Requisitos:
1. Validação de estoque (quantidade máxima)
2. Salvar pedido no localStorage
3. Histórico de pedidos

## 5. Recursos Adicionais

- [MDN - Validação de Formulários](https://developer.mozilla.org/pt-BR/docs/Learn/Forms/Form_validation)
- [MDN - Web Storage API](https://developer.mozilla.org/pt-BR/docs/Web/API/Web_Storage_API)
- [MDN - RegExp](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Guide/Regular_Expressions)
- [Biblioteca InputMask](https://github.com/RobinHerbots/Inputmask)
- [Biblioteca ValidatorJS](https://github.com/validatorjs/validator.js)
