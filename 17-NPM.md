# Gerenciamento de Pacotes em JavaScript - NPM (Node Package Manager)

## Introdução ao NPM

O NPM (Node Package Manager) é o gerenciador de pacotes padrão para JavaScript e Node.js. Ele permite:

- Instalar e gerenciar dependências
- Compartilhar código com outros desenvolvedores
- Controlar versões de bibliotecas
- Executar scripts de automação

## Instalação

O NPM vem instalado automaticamente com o Node.js:

```bash
# Verificar versão do NPM
npm -v

# Atualizar NPM
npm install -g npm@latest
```

## Inicializando um Projeto

```bash
# Criar package.json interativamente
npm init

# Criar package.json com valores padrão
npm init -y
```

### Anatomia do package.json

```json
{
  "name": "meu-projeto",
  "version": "1.0.0",
  "description": "Descrição do projeto",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.7"
  }
}
```

## Gerenciando Dependências

### Instalação de Pacotes

```bash
# Instalar e salvar como dependência
npm install nome-do-pacote

# Instalar como dependência de desenvolvimento
npm install nome-do-pacote --save-dev

# Instalar globalmente
npm install -g nome-do-pacote

# Instalar versão específica
npm install nome-do-pacote@1.2.3
```

### Versionamento Semântico (SemVer)

- **Major.Minor.Patch** (ex: 2.4.1)
  - Major: mudanças incompatíveis
  - Minor: novas funcionalidades compatíveis
  - Patch: correções de bugs

### Prefixos de Versão

- `^`: aceita atualizações de minor e patch
- `~`: aceita apenas atualizações de patch
- `*`: aceita qualquer versão
- `>`: maior que
- `>=`: maior ou igual
- `<`: menor que
- `<=`: menor ou igual

## Scripts NPM

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "build": "webpack",
    "test": "jest"
  }
}
```

Executando scripts:
```bash
npm run script-name
```

## node_modules e package-lock.json

### node_modules
- Diretório onde os pacotes são instalados
- Deve ser incluído no .gitignore
- Recriado com `npm install`

### package-lock.json
- Garante consistência nas instalações
- Registra versões exatas das dependências
- Deve ser versionado

## Comandos Importantes

```bash
# Listar pacotes instalados
npm list

# Atualizar pacotes
npm update

# Remover pacote
npm uninstall nome-do-pacote

# Auditar segurança
npm audit

# Corrigir vulnerabilidades
npm audit fix

# Limpar cache
npm cache clean --force
```

## Boas Práticas

1. **Versionamento**
   - Sempre use package-lock.json
   - Especifique versões precisas para dependências críticas

2. **Segurança**
   - Execute `npm audit` regularmente
   - Mantenha pacotes atualizados
   - Use `npm audit fix` com cautela

3. **Organização**
   - Separe dependências de desenvolvimento
   - Documente scripts importantes
   - Mantenha o package.json organizado

4. **Performance**
   - Use `npm ci` em ambientes de CI/CD
   - Limpe node_modules periodicamente
   - Evite instalações globais desnecessárias

## Alternativas ao NPM

1. **Yarn**
   - Mais rápido em algumas operações
   - Cache offline
   - Determinístico

2. **pnpm**
   - Economia de espaço em disco
   - Mais rápido que npm e yarn
   - Links simbólicos eficientes

## Resolução de Problemas Comuns

1. **Conflitos de Versão**
```bash
npm dedupe
```

2. **Módulos Corrompidos**
```bash
# Limpar e reinstalar
rm -rf node_modules
npm cache clean --force
npm install
```

3. **Erro de Permissão**
```bash
# Linux/Mac
sudo npm install -g nome-do-pacote
```

## Recursos Adicionais

- [Documentação Oficial do NPM](https://docs.npmjs.com/)
- [NPM Best Practices](https://docs.npmjs.com/cli/v8/using-npm/developers)
- [Semantic Versioning](https://semver.org/)
