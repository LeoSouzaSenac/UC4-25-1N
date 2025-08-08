# Condicionais em TypeScript

Em TypeScript (e JavaScript), as estruturas condicionais são usadas para tomar decisões no código com base em diferentes condições. Neste guia, vamos aprender:

- `if`
- `if...else`
- `else if`
- Operador ternário
- `switch`
- Criar um menu no terminal com `switch` + `readline-sync`

---

## 1. `if`

A estrutura `if` avalia uma condição e executa o bloco de código se ela for verdadeira.

```ts
const idade = 18;

if (idade >= 18) {
  console.log("Você é maior de idade.");
}
````

---

## 2. `if...else`

Usado quando você quer uma ação para verdadeiro e outra para falso.

```ts
const estaChovendo = true;

if (estaChovendo) {
  console.log("Leve um guarda-chuva.");
} else {
  console.log("Pode sair tranquilo.");
}
```

---

## 3. `else if`

Permite verificar múltiplas condições.

```ts
const nota = 7;

if (nota >= 9) {
  console.log("Excelente!");
} else if (nota >= 7) {
  console.log("Bom!");
} else {
  console.log("Precisa melhorar.");
}
```

---

## 4. Operador Ternário

Uma forma curta de escrever `if...else`.

```ts
const pontuacao = 85;

const resultado = pontuacao >= 60 ? "Aprovado" : "Reprovado";

console.log(resultado); // "Aprovado"
```

### Sintaxe:

```ts
condição ? valorSeVerdadeiro : valorSeFalso
```

---

## 5. `switch`

O `switch` é útil quando você tem múltiplos valores para comparar com a mesma variável.

```ts
const fruta = "maçã";

switch (fruta) {
  case "banana":
    console.log("Banana é rica em potássio.");
    break;
  case "maçã":
    console.log("Maçã ajuda na digestão.");
    break;
  case "laranja":
    console.log("Laranja tem muita vitamina C.");
    break;
  default:
    console.log("Fruta desconhecida.");
}
```

> ⚠️ Sempre use `break` para evitar que os casos continuem sendo executados em sequência.

---

## 6. Criando um **menu no terminal** com `switch` e `readline-sync`

Você pode criar menus interativos no terminal usando a biblioteca `readline-sync`.

### Instalação:

```bash
npm install readline-sync
npm install @types/readline-sync
```

### Exemplo de menu:

```ts
import * as readline from 'readline-sync';

console.log("=== MENU PRINCIPAL ===");
console.log("1 - Olá");
console.log("2 - Sobre");
console.log("3 - Sair");

const opcao = readline.question("Escolha uma opção: ");

switch (opcao) {
  case "1":
    console.log("Olá! Seja bem-vindo!");
    break;
  case "2":
    console.log("Este é um exemplo de menu com switch.");
    break;
  case "3":
    console.log("Saindo...");
    break;
  default:
    console.log("Opção inválida.");
}
```

---

## Resumo

| Estrutura           | Uso principal                               |
| ------------------- | ------------------------------------------- |
| `if`                | Verifica uma condição única                 |
| `if...else`         | Ação alternativa caso a condição seja falsa |
| `else if`           | Verificar várias condições em sequência     |
| `operador ternário` | Atalho para `if...else` simples             |
| `switch`            | Comparar um valor com múltiplos casos       |

---

## Exercícios

### 1. **`if...else` – Tema: Clima**

```ts
// Se estiver chovendo, diga para levar guarda-chuva.
// Se não, diga que está um bom dia para caminhar.

const estaChovendo = true;
```

---

### 2. **Operador Ternário – Tema: Escola**

```ts
// Se a nota for >= 6, "Aprovado", senão "Reprovado"

const nota = 7;
```

---

### 3. **`switch` – Tema: Animais**

```ts
// Crie um switch que responda com:
// "Au au" para "cachorro"
// "Miau" para "gato"
// "Desconhecido" para qualquer outro

const animal = 'gato';
```

---

### 4. **Menu com readline-sync – Tema: Jogo**

```ts
// Crie um menu com opções:
// 1 - Jogar
// 2 - Carregar Jogo
// 3 - Sair

// Importe readline-sync e use switch para mostrar uma mensagem para cada opção.
```

---

## 🧠 Dicas finais

* Use `if` para decisões simples.
* Use `switch` quando tiver várias opções fixas.
* Use operador ternário para expressões curtas e simples.
* Nunca se esqueça dos `break` nos `case` de `switch`.
* O `readline-sync` é ótimo para criar experiências interativas no terminal!

---


Se quiser, posso exportar isso como um arquivo `.md` direto para você baixar. Deseja isso?
```
