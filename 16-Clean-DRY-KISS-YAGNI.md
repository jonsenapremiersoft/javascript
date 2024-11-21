# Clean Code: Escrevendo Código Limpo com JavaScript

## Introdução

Clean Code (Código Limpo) é uma filosofia de desenvolvimento que visa criar código mais legível, manutenível e escalável. Nesta aula, abordaremos os principais conceitos e princípios, usando JavaScript como linguagem de exemplo.

## Índice
1. [Nomenclatura](#nomenclatura)
2. [Funções](#funcoes)
3. [DRY (Don't Repeat Yourself)](#dry)
4. [KISS (Keep It Simple, Stupid)](#kiss)
5. [YAGNI (You Aren't Gonna Need It)](#yagni)

## Nomenclatura

A nomenclatura adequada é fundamental para um código limpo. Nomes devem ser descritivos e revelar a intenção.

### ❌ Como NÃO fazer:

```javascript
const d = new Date(); // d não diz nada sobre o propósito
const arr = ['João', 'Maria', 'Pedro']; // arr é muito genérico
const x = user.age > 18; // x não indica o que está sendo verificado

function calc(a, b) { // Nome e parâmetros não descritivos
    return a + b;
}
```

### ✅ Como fazer:

```javascript
const currentDate = new Date();
const studentNames = ['João', 'Maria', 'Pedro'];
const isUserAdult = user.age > 18;

function calculateTotalPrice(basePrice, taxRate) {
    return basePrice + taxRate;
}
```

### Regras para boa nomenclatura:
- Use substantivos para variáveis e objetos
- Use verbos para funções
- Seja específico e evite abreviações
- Use nomes pronunciáveis
- Siga o padrão camelCase para JavaScript

## Funções

Funções são blocos fundamentais do código. Devem ser pequenas, fazer apenas uma coisa e fazer bem.

### ❌ Como NÃO fazer:

```javascript
function processUser(user) {
    // Função fazendo muitas coisas
    if (!user.name || !user.email) {
        throw new Error('Dados inválidos');
    }
    
    const age = calculateAge(user.birthDate);
    user.age = age;
    
    if (user.age >= 18) {
        user.canDrive = true;
    }
    
    if (user.type === 'premium') {
        calculateDiscount(user);
    }
    
    saveUser(user);
    sendWelcomeEmail(user);
    
    return user;
}
```

### ✅ Como fazer:

```javascript
function processUser(user) {
    validateUserData(user);
    enrichUserWithAge(user);
    checkDrivingEligibility(user);
    applyPremiumBenefits(user);
    return saveAndNotifyUser(user);
}

function validateUserData(user) {
    if (!user.name || !user.email) {
        throw new Error('Dados inválidos');
    }
}

function enrichUserWithAge(user) {
    user.age = calculateAge(user.birthDate);
}

function checkDrivingEligibility(user) {
    user.canDrive = user.age >= 18;
}

function applyPremiumBenefits(user) {
    if (user.type === 'premium') {
        calculateDiscount(user);
    }
}

function saveAndNotifyUser(user) {
    saveUser(user);
    sendWelcomeEmail(user);
    return user;
}
```

## DRY (Don't Repeat Yourself)

DRY é um princípio que visa eliminar a duplicação de código. Código duplicado é difícil de manter e propenso a erros.

### ❌ Como NÃO fazer:

```javascript
function calculateStudentGrade(student) {
    const total = student.tests.reduce((sum, test) => sum + test, 0);
    const average = total / student.tests.length;
    
    if (average >= 9) return 'A';
    if (average >= 8) return 'B';
    if (average >= 7) return 'C';
    if (average >= 6) return 'D';
    return 'F';
}

function calculateTeacherRating(teacher) {
    const total = teacher.ratings.reduce((sum, rating) => sum + rating, 0);
    const average = total / teacher.ratings.length;
    
    if (average >= 9) return 'Excelente';
    if (average >= 8) return 'Ótimo';
    if (average >= 7) return 'Bom';
    if (average >= 6) return 'Regular';
    return 'Insatisfatório';
}
```

### ✅ Como fazer:

```javascript
function calculateAverage(numbers) {
    const total = numbers.reduce((sum, num) => sum + num, 0);
    return total / numbers.length;
}

function getGradeFromAverage(average, scaleType = 'letter') {
    const scales = {
        letter: {
            9: 'A',
            8: 'B',
            7: 'C',
            6: 'D',
            0: 'F'
        },
        description: {
            9: 'Excelente',
            8: 'Ótimo',
            7: 'Bom',
            6: 'Regular',
            0: 'Insatisfatório'
        }
    };

    const thresholds = Object.keys(scales[scaleType])
        .map(Number)
        .sort((a, b) => b - a);

    const grade = thresholds.find(threshold => average >= threshold);
    return scales[scaleType][grade];
}

function calculateStudentGrade(student) {
    const average = calculateAverage(student.tests);
    return getGradeFromAverage(average, 'letter');
}

function calculateTeacherRating(teacher) {
    const average = calculateAverage(teacher.ratings);
    return getGradeFromAverage(average, 'description');
}
```

## KISS (Keep It Simple, Stupid)

KISS enfatiza a importância da simplicidade no código. Soluções simples são mais fáceis de entender e manter.

### ❌ Como NÃO fazer:

```javascript
function getDayType(date) {
    const day = date.getDay();
    let type;
    
    if (day === 0 || day === 6) {
        const isHoliday = checkIfHoliday(date);
        if (isHoliday) {
            if (isSpecialHoliday(date)) {
                type = 'special_holiday';
            } else {
                type = 'regular_holiday';
            }
        } else {
            type = 'weekend';
        }
    } else {
        const isHoliday = checkIfHoliday(date);
        if (isHoliday) {
            if (isSpecialHoliday(date)) {
                type = 'special_holiday';
            } else {
                type = 'regular_holiday';
            }
        } else {
            type = 'weekday';
        }
    }
    
    return type;
}
```

### ✅ Como fazer:

```javascript
function getDayType(date) {
    if (isSpecialHoliday(date)) {
        return 'special_holiday';
    }
    
    if (checkIfHoliday(date)) {
        return 'regular_holiday';
    }
    
    return isWeekend(date) ? 'weekend' : 'weekday';
}

function isWeekend(date) {
    const day = date.getDay();
    return day === 0 || day === 6;
}
```

## YAGNI (You Aren't Gonna Need It)

YAGNI nos lembra de não adicionar funcionalidades até que sejam realmente necessárias.

### ❌ Como NÃO fazer:

```javascript
class User {
    constructor(name, email) {
        this.name = name;
        this.email = email;
        this.loginHistory = []; // Ainda não necessário
        this.preferences = {}; // Ainda não necessário
        this.friendsList = []; // Ainda não necessário
    }

    async save() {
        await this.backupData(); // Ainda não necessário
        await this.validateSocialMedia(); // Ainda não necessário
        await this.syncWithCloud(); // Ainda não necessário
        
        return await database.save(this);
    }
}
```

### ✅ Como fazer:

```javascript
class User {
    constructor(name, email) {
        this.name = name;
        this.email = email;
    }

    async save() {
        return await database.save(this);
    }
}
```

## Exercício

1. Refatore o seguinte código aplicando os princípios aprendidos:

```javascript
function calcPrice(user) {
    const date = new Date();
    let price;
    if (user.type === 'premium') {
        price = 100;
        if (date.getDay() === 0) {  // domingo
            price = price * 0.8;  // desconto de 20%
        }
    } else {
        price = 150;
        if (date.getDay() === 0) {  // domingo
            price = price * 0.9;  // desconto de 10%
        }
    }
    return price;
}
```

2. Identifique os problemas no código acima e explique como cada princípio (Clean Code, DRY, KISS, YAGNI) poderia ser aplicado para melhorá-lo. Alguns problemas evidentes incluem:

- Nomes de variáveis pouco descritivos
- Repetição da lógica de verificação de domingo
- Números mágicos (100, 150, 0.8, 0.9)
- Função fazendo múltiplas coisas

## Conclusão

Lembre-se sempre:
1. Código limpo é código que pode ser entendido facilmente por outros desenvolvedores
2. Nomes significativos economizam tempo de compreensão
3. Funções devem fazer apenas uma coisa
4. Não se repita (DRY)
5. Mantenha as coisas simples (KISS)
6. Não adicione funcionalidades até precisar delas (YAGNI)

## Solução do Exercício

```javascript
function calculateUserPrice(user) {
    const PREMIUM_BASE_PRICE = 100;
    const REGULAR_BASE_PRICE = 150;
    
    const basePrice = user.type === 'premium' 
        ? PREMIUM_BASE_PRICE 
        : REGULAR_BASE_PRICE;
    
    return applySundayDiscount(basePrice, user.type);
}

function applySundayDiscount(price, userType) {
    if (!isSunday()) return price;
    
    const discountRate = userType === 'premium' ? 0.8 : 0.9;
    return price * discountRate;
}

function isSunday() {
    return new Date().getDay() === 0;
}
```

Melhorias aplicadas:
1. Clean Code: Nomes significativos e funções com responsabilidade única
2. DRY: Lógica de verificação do domingo extraída para função própria
3. KISS: Estrutura simplificada e fácil de entender
4. YAGNI: Apenas as funcionalidades necessárias foram implementadas
